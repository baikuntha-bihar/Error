# Error
Error

apiVersion: v1
kind: ConfigMap
metadata:
  name: {{ .Release.Name }}-{{ .Values.configMap.nameSuffix }}
  namespace: {{ .Release.Namespace }}
  labels:
    {{ include "Epay_Payment_Service.labels" . | nindent 4 }}
{{ if $.Values.configMap.additionalLabels }}
    {{ toYaml $.Values.configMap.additionalLabels | nindent 4 }}
{{ end }}
{{ if $.Values.configMap.annotations }}
  annotations:
    {{ toYaml $.Values.configMap.annotations | nindent 4 }}
{{ end }}
data:
  application.properties: |
    spring.application.name=epay_payment_service
    server.port=9093   
    server.servlet.context-path=/api/payments/v1/

    # Db connectivity
    spring.jpa.show-sql=true
    spring.jpa.properties.hibernate.show_sql=true
    spring.jpa.properties.hibernate.format_sql=true
    spring.web.resources.static-locations=classpath:/,file:/non-existent-folder
    #logging.level.org.springframework.web=debug

    #spring.datasource.url=jdbc:oracle:thin:@10.177.135.4:1590:epaysit2
    #spring.datasource.url=jdbc:oracle:thin:@10.177.135.1:1590:newuat1
    spring.datasource.url=jdbc:oracle:thin:@(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=epaydbscanuat.sbiepay.sbi)(PORT=1524))(CONNECT_DATA= (SERVER=DEDICATED) (SERVICE_NAME=newuat)))
    # spring.datasource.username=PAYAGGTRANSCTION
    # spring.datasource.password=SIA#2025
    spring.datasource.username=${DB_USERNAME}
    spring.datasource.password=${DB_PASSWORD}
    spring.jpa.show-sql=true

    spring.datasource.driver-class-name=oracle.jdbc.OracleDriver
    
    #Application Proxy Details
    https_protocols = TLSv1.2
    https_proxySet = true
    https_proxyHost = serverswg.sbi.co.in
    https_proxyPort = 9090

    # Optional settings
    spring.datasource.hikari.maximum-pool-size=10
    spring.datasource.hikari.minimum-idle=5
    spring.datasource.hikari.idle-timeout=30000
    spring.datasource.hikari.max-lifetime=2000000

    #In Minutes
    transaction.token.expiry.time=30

    # Liquibase Properties
    spring.liquibase.change-log=classpath:db/changelog/db.changelog-master.xml
    spring.liquibase.enabled=false
    spring.liquibase.drop-first=false
    logging.level.liquibase=DEBUG

    spring.jpa.hibernate.ddl-auto=none

    #jwt.secret.key=K98JUXrheTIDbUJcK312nith7i74bFJSjMF2v0tcuv4VKKu9DCCZrXBXVR5OAsXojKOsmWEAtVl4r7xa935i3g==
    #security.whitelist.url=/webjars/, /actuator/, /swagger-resources/, /v3/api-docs, /swagger-ui/, /swagger-ui.html, /v1/token/access


    
    #WIBMO PG Constants
    epay.payment.card.callback_url = https://uat.epay.sbi/api/payments/v1/cards/sbi/visamaster/callback
    epay.payment.card.callbackg_url_rupay = https://uat.epay.sbi/api/payments/v1/cards/sbi/rupay/callback
    epay.payment.card.callback_url_intl = https://uat.epay.sbi/api/payments/v1/cards/sbi/intl/visamaster/callback
    epay.payment.card.callbackg_url_rupay_intl = https://uat.epay.sbi/api/payments/v1/cards/sbi/intl/rupay/callback
    epay.payment.card.pvReqURL = https://3ds2-api-3dsserver-intg.pc.enstage-sas.com/3dsserverapi/v5/pVrq/8642/
    epay.payment.card.saleAuthURL = https://areionsbi.pc.enstage-sas.com/saleservice/api/v1/sale
    epay.payment.card.checkbin_Url = https://areionsbi.pc.enstage-sas.com/authentication/api/v1/checkbin
    epay.payment.card.initiate_url = https://areionsbi.pc.enstage-sas.com/authentication/api/v1/initiate
    epay.payment.card.generateOtp_url = https://areionsbi.pc.enstage-sas.com/authentication/api/v1/generateOtp
    epay.payment.card.resendOtp_url = https://areionsbi.pc.enstage-sas.com/authentication/api/v1/resendOtp
    epay.payment.card.verifyOtp_url = https://areionsbi.pc.enstage-sas.com/authentication/api/v1/verifyOtp
    epay.payment.card.authorize_url = https://areionsbi.pc.enstage-sas.com/saleservice/api/v1/authorize
    epay.payment.card.reverse_url = https://areionsbi.pc.enstage-sas.com/authentication/web/v1/parseRupayResponse
    epay.payment.card.preAuth_url = https://areionsbi.pc.enstage-sas.com/saleservice/api/v1/preauth
    epay.payment.card.token_url = https://cardvault-azure.pc.enstage-sas.com/tokenVault/v3/tokenize

    epay.payment.card.api_key = 849ca23e-b115-11ed-a376-005056b59d84
    epay.payment.card.clientId = 175f0289-0272-4cd2-bffa-51fc9b6c4101
    epay.payment.card.clientApiUser = 100001-HDFC-2lP6tK9sB7
    epay.payment.card.clientApiKey = HDFC5nN2pO3aR5
    epay.payment.card.tokenSecretKey = f3a81ff0-e139-4e6a-8888-9709a0407713
    epay.payment.card.tokenSecretKey_1 = c19215e2-c2a4-4630-937b-a3bfd764c96b
    epay.payment.card.merchantId_Token = hdfctestmid1
    epay.payment.card.tokenRequesterId_MC = 7D6D61B2-0BF9-4763-885F-6E9D7516C00E
    epay.payment.card.tokenRequesterId_VS = DFFFAC4C-B2D8-4CEA-BEBB-E7EB1716A348
    epay.payment.card.tokenRequesterId_R = 77799966611
    epay.payment.card.acquiringBankId = 93734895
    epay.payment.card.acquireInstanceId = 93954c92-58ed-4912-8648-0948d5becc69
    epay.payment.card.acquirerMerchantId = PAYUGCMID1

        

