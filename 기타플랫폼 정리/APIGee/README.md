-- APIgee 사용법

1. 토큰 발급
2. api호출에 토큰 정보 입력
3. api호출 및 반환


APIgee 흐름도
![image](apigee.png) 


1.토큰 받아 오기
 ```java
@Value("#{applicationProp['apigee.arn']}") //접근을 위한 ARN 정보
private String secretArn;

//토큰 받기위한 함수 생성
// paxClientId,paxClientSecret 정보를 호출 token갑 반환
public void apigeeUpdateCheck(){
   try{
      // 4시간 단위로 갱신
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

//실제 토큰 호출 및 반환부분
public String getToken(String clientId, String clientSecret) throws Exception{

    String credentials = clientId + ":" + clientSecret;
    String encodedCredentials = new String(Base64.encode(credentials.getBytes()));

    URL url = new URL(tokenUrl);
    HttpURLConnection connection = (HttpURLConnection) url.openConnection();
    connection.setRequestMethod("POST");
    connection.setRequestProperty("Authorization", "Basic " + encodedCredentials);
    connection.setRequestProperty("Content-Type", "application/x-www-form-urlencoded");
    connection.setDoOutput(true);

    String requestBody = "grant_type=client_credentials";
    connection.getOutputStream().write(requestBody.getBytes());

    int responseCode = connection.getResponseCode();
    if (responseCode == HttpURLConnection.HTTP_OK) {
        BufferedReader in = new BufferedReader(new InputStreamReader(connection.getInputStream()));
        String accessToken= null;
        String tokenType= null;
        String inputLine;
        while ((inputLine = in.readLine()) != null) {
            if (inputLine.contains("access_token")) {
                accessToken = inputLine.substring(inputLine.indexOf(":")+1).replaceAll("\"", "").replaceAll(",", "").trim();
            }
        }
        in.close();
        return accessToken;
    }else{
        return null;
    }
}
 ```
