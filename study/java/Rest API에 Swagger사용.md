## Rest API에 Swagger 사용

Swagger란?
- Open API 개발시 API문서를 자동으로 생성해 주는 프레임워크.

장점
- API 연동규격서를 문서화 하면 시간이 갈수록 소스와 싱크가 안 맞는 문제 발생.
- 별도의 연동테스트 Tool(Rest Console,Post Man)등을 사용 안하고 테스트 가능.

Swagger Maven 추가
~~~xml
<!-- swagger -->
<dependency>
    <groupId>io.springfox</groupId>
    <artifactId>springfox-swagger2</artifactId>
    <version>2.2.2</version>
</dependency>
<!-- swagger UI-->
<dependency>
    <groupId>io.springfox</groupId>
    <artifactId>springfox-swagger-ui</artifactId>
    <version>2.2.2</version>
</dependency>
~~~

설정
~~~java
@Configuration
@EnableSwagger2
public class SwaggerConfig{
    @Bean
    public Docket api() {
        return new Docket(DocumentationType.SWAGGER_2)
                .select().apis(RequestHandlerSelectors.any())
                .paths(PathSelectors.any())
                .build()
                .apiInfo(apiInfo());
    }
     
     
    @SuppressWarnings("deprecation")
    private ApiInfo apiInfo() {
        ApiInfo apiInfo = new ApiInfo(
                                "Rest API Sample",
                                "Rest API 샘플입니다.",
                                "0.1",
                                "https://github.com/opang601",
                                "opang601@gmail.com",
                                "License of API",
                                "https://github.com/opang601");
        return apiInfo;
    }
 
}
~~~

Controller 에서 내용 정의

~~~java
@RestController
@RequestMapping("/sell")
public class SellController {
    private Logger logger = LoggerFactory.getLogger(getClass());
     
    @Autowired
    private SellRepository sellRepository;
    @Autowired
    private OrderSheetRepository orderSheetRepository;
     
    @ApiOperation(value="주문조회", notes="주문 조회 API입니다.")
    @GetMapping("/info/{sIdx}")
    public SellEntity getSellInfo(@ApiParam(value="주문번호",required=true, defaultValue="1") @PathVariable String sIdx) {
        SellEntity sellEntity = sellRepository.findOne(sIdx);
        logger.info("Sell Info : {}",sellEntity.toString());
        return sellEntity;
    }
     
    @ApiOperation(value="주문 정보 페이징 조회", notes="주문 정보 페이징 처리 API입니다.")
    @GetMapping("/sellPaging")
    public List<SellEntity> getSellPaging(@ApiParam(value="페이지 번호",required=true, defaultValue="0") @RequestParam int page,
                                          @ApiParam(value="페이지 사이즈",required=true, defaultValue="10") @RequestParam int size) {
         
        PageRequest pageable = new PageRequest(page, size, Direction.DESC, "sIdx");
        Page<SellEntity> sellSheetList =  sellRepository.findAll(pageable);
        logger.info("SellEntity Info : {}",sellSheetList.toString());
 
        return sellSheetList.getContent();
    }
 
    @ApiOperation(value="장바구니 조회", notes="장바구니 조회 API입니다.")
    @GetMapping("/ordersheet/{orderNum}")
    public List<OrderSheetEntity> getOrderSheetInfo(@ApiParam(value="주문번호",required=true, defaultValue="828443") @PathVariable String orderNum) {
         
        Specifications<OrderSheetEntity> specs = Specifications.where(OrderSheetSpecs.eqaulOrderNum(orderNum));
        List<OrderSheetEntity> orderSheetList =  orderSheetRepository.findAll(specs);
        logger.info("OrderSheet Info : {}",orderSheetList.toString());
        return orderSheetList;
    }
}
~~~