-- APIgee 사용법

1. 토큰 발급
2. api호출에 토큰 정보 입력
3. api호출 및 반환


APIgee 흐름도
![image](apigee.png) 


1.토큰 받아 오기
--
@Value("#{applicationProp['apigee.arn']}")
private String secretArn;

public void apigeeUpdateCheck(){
   try{
      if (paxUpdateDate == null || Duration.between(paxUpdateDate, LocalDateTime.now()).toHours() >= 4){
         String secretIDKEY = apiGeeService.getSecretIDKEY(secretArn).replaceAll(",", ":");
         String[] spliet = secretIDKEY.split(":");
         paxClientId = spliet[1].replaceAll("\"", "").replaceAll("}", "");
         paxClientSecret = spliet[3].replaceAll("\"", "").replaceAll("}", "");
         paxUpdateDate = LocalDateTime.now();
         paxApigeeToken = apiGeeService.getToken(paxClientId, paxClientSecret);
      }
   }catch (Exception e){
      log.error(e.toString());
      paxApigeeToken = null;
   }
}
--
