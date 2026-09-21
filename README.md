# Error
Error



server:
  port: 9095
  servlet:
    context-path: /payments/v1/

spring:
  application:
    name: epay_payment_service
  messages:
    basename: errors,messages
  jpa:
    show-sql: true
    database-platform: org.hibernate.dialect.OracleDialect
    hibernate:
      ddl-auto: none
    properties:
      hibernate:
        show_sql: true
        format_sql: true
  web:
    resources:
      static-locations: classpath:/,file:/non-existent-folder
  datasource:
    url: jdbc:oracle:thin:@10.177.134.124:1590:epaydbdev1
    username:
    password:
    driver-class-name: oracle.jdbc.OracleDriver
    hikari:
      maximum-pool-size: 10
      minimum-idle: 5
      idle-timeout: 30000
      max-lifetime: 2000000
      connection-timeout: 30000
  liquibase:
    change-log: classpath:db/changelog/db.changelog-master.xml
    enabled: true
    drop-first: false
  mail:
    host: 10.176.245.236
    port: 587
    username: sbitestclient
    password: sbitestclient_7f827c4b3aa6cd1f08d6b9cce2c0c80e
  kafka:
    bootstrapServers: dev-cluster-kafka-bootstrap-dev-kafka.apps.dev.sbiepay.sbi:443
    topic:
      partitions: 4
      replicationFactor: 1
      payment:
        notification:
          sms: local_payment_sms_notification_topic
          email: local_payment_email_notification_topic
          cashstatusquery: payment_cashstatusquery_notification_topic
        cashstatusquery:
          cron_time: '0/60 * * * * *'
    consumer:
      groupId: gatewayOfflinePooling-consumers
      enableAutoCommit: true
      autoCommitInterval: 100
      sessionTimeoutMS: 300000
      requestTimeoutMS: 420000
      fetchMaxWaitMS: 200
      maxPollRecords: 5
      autoOffsetReset: latest
      keyDeserializer: org.apache.kafka.common.serialization.StringDeserializer
      valueDeserializer: org.apache.kafka.common.serialization.StringDeserializer
      retryMaxAttempts: 3
      retryBackOffInitialIntervalMS: 10000
      retryBackOffMaxIntervalMS: 30000
      numberOfConsumers: 1
    producer:
      acks: all
      retries: 3
      batchSize: 1000
      lingerMs: 1
      bufferMemory: 33554432
      keyDeserializer: org.apache.kafka.common.serialization.StringSerializer
      # Note: 'StringSerialize' is kept exactly as in the original properties file
      valueDeserializer: org.apache.kafka.common.serialization.StringSerialize
    properties:
      ssl:
        truststore:
          location: C:/certs/kafka/dev-cluster-cluster-ca-cert.p12
          password: Xe8FrxOGVAx
          type: PKCS12
        keystore:
          location: C:/certs/kafka/dev-cluster-clients-ca-cert.p12
          password: J55FITkgEFid
          type: PKCS12

logging:
  level:
    liquibase: DEBUG
    org:
      apache:
        kafka: OFF
      springframework:
        kafka: OFF

merchantOrderPayments:
  token:
    expiry:
      time: 30

https_protocols: TLSv1.2
https_proxySet: true
https_proxyHost: serverswg.sbi.co.in
https_proxyPort: 9090

epay:
  payment:
    sbiinb:
      aek: BiIZ5feKr16Td3XSpVyqwXlwRNfSy9Gtis04WqEbD/0=
      mek: xSUnsXbNEZPochZmrombg5NqEDQAsWxowx+WmDSb2lyocZrsShk7DUL0N89fORoIwkZVCZI/hWhS95Sw
      kek: lZiUYRr3E3tZBZJECefddgTB06jl0RAXaBjOHF1KLSMxKhBhPsXlpnKNI7XGzsHgTi0u6o9k4Q1YmZW
      sbiinbKey: resources/keys/SBI_EPAY.key
      meCode: SBIEPAY
      dvURL: SBIEPAY
      bankURL: https://uatmerchant.onlinesbi.sbi
      bankbrowserurl: https://merchantuat.onlinesbi.sbi/merchant/merchantprelogin.htm
      bankdvurl: https://merchantuat.onlinesbi.sbi/thirdparties/doubleverification.htm
      keyvalue: encdata
      merchantcode: SBIEPAY2
      paymentsRedirectUrl: /payments/v1/sbi/inb/responseRedirect?status=
      devredirecturl: https://dev.epay.sbi/2.0/channel/inb/sbi/
      cancelurl: https://dev.epay.sbi/payments/v1/sbi/inb/callback
      sbiredirecturl: https://dev.epay.sbi/payments/v1/sbi/inb/callback
      otherinbstatusquery: https://uat.sbiepay.sbi/payagg/statusQuery/getStatusQuery
      gtwmapid:
    wallet:
      cancelurl: https://dev.epay.sbi/api/payments/v1/wallet/sbi/mobikwikcallback
      sbiredirectdvurl: https://dev.epay.sbi/api/payments/v1/wallet/sbi/mobikwikcallback
      bankbrowserurl: https://test.mobikwik.com/encwallet
      bankdvurl: https://test.mobikwik.com/enccheckstatus
      mid: MBK1034202
      cell: 7039262141
      email: punam.rajput.cedge@sbi.co.in
      merchantname: Test
      secretkey: ju6tygh7u7tdg554k098ujd5468o
      encryptionkey: 1234567890123456
      Statuscode: 0
      statusmessage: The payment has been successfully collected
      refid: 838731552
      bridgePublicKey:
      cscbankbrowserurl: https://payuat.csccloud.in/v1/payment/
      cscbankdvurl: https://bridgeuat.csccloud.in/cscbridge/v2/transaction/status/format/json
      apiKey: 5dc9302c9f3dbe952e31e73406bd45a6
      productid: '1751396615'
      merchantid: '17513'
      cscid: '500100100014'
      bridgePrivateKey:
      keyvalue: messag
    otherinb:
      success:
        base:
          path: https://www.sbiepay.sbi
      fail:
        base:
          path: https://www.sbiepay.sbi
      mid: 1000524
      key: A3FZ8NvgJN4IjD20YtYQQfEN83Ej13rOVNYm38Prtpo=
      merchant_post_url: https://uat.sbiepay.sbi/secure/MerchantHostedListener
      proxyip: 10.176.172.160
      proxyport: 3066
      tlsversion: TLSv1.2
      key_browser: ''
    card:
      callback_url: https://dev.epay.sbi/api/payments/v1/cards/sbi/visamaster/callback
      callbackg_url_rupay: https://dev.epay.sbi/api/payments/v1/cards/sbi/rupay/callback
      callback_url_intl: https://dev.epay.sbi/api/payments/v1/cards/sbi/intl/visamaster/callback
      callback_url_rupay_intl: https://dev.epay.sbi/api/payments/v1/cards/sbi/intl/rupay/callback
      pvReqURL: https://3ds2-api-3dsserver-intg.pc.enstage-sas.com/3dsserverapi/v5/pVrq/8642/
      saleAuthURL: https://areionsbi.pc.enstage-sas.com/saleservice/api/v1/sale
      checkbin_Url: https://areionsbi.pc.enstage-sas.com/authentication/api/v1/checkbin
      initiate_url: https://areionsbi.pc.enstage-sas.com/authentication/api/v1/initiate
      generateOtp_url: https://areionsbi.pc.enstage-sas.com/authentication/api/v1/generateOtp
      resendOtp_url: https://areionsbi.pc.enstage-sas.com/authentication/api/v1/resendOtp
      verifyOtp_url: https://areionsbi.pc.enstage-sas.com/authentication/api/v1/verifyOtp
      authorize_url: https://areionsbi.pc.enstage-sas.com/saleservice/api/v1/authorize
      reverse_url: https://areionsbi.pc.enstage-sas.com/authentication/web/v1/parseRupayResponse
      token_url: https://cardvault-azure.pc.enstage-sas.com/tokenVault/v3/tokenize
      api_key: 849ca23e-b115-11ed-a376-005056b59d84
      clientId: 175f0289-0272-4cd2-bffa-51fc9b6c4101
      clientApiUser: 100001-HDFC-21P6tK9sB7
      clientApiKey: HDFC5nN2pO3aR5
      tokenSecretKey: f3a81ff0-e139-4e6a-8888-9709a0407713
      tokenSecretKey_1: c19215e2-c2a4-4630-937b-a3bfd764c96b
      merchantId_Token: hdfctestmid1
      tokenRequesterId_MC: 7D6D61B2-0BF9-4763-885F-6E9D7516C00E
      tokenRequesterId_VS: DFFAC4C-B2D8-4CEA-BEBB-E7EB1716A348
      tokenRequesterId_R: '77799966611'
      acquiringBankId: 93734895
      acquireInstanceId: 93954c92-58ed-4912-8648-0948d5becc69
      acquirerMerchantId: PAYUGCMID1
      pgInstanceId_1: 8642
      pgInstanceId: 72702415
      pgInstanceId_2: 72702415
      pgInstanceId_3: 9999
      acquirerBIN_MASTER: 597291
      acquirerBIN_VISA: 401934
      acquirerID: 8642
      MCC: 4900
      transactionTypeCode: 9003
      deviceCategory: 0
      deviceChannel: '02'
      p_messageVersion: 2.1.0
      messageCategory: '01'
      vaultId: 100001
      INR: 356
      USD: 840
      proxySet: true
      browserAgent: TestMerchant/26.5.0.100 (Android/13/SM-S908E)
      paymentsRedirectUrl: https://dev.epay.sbi/ui/channel/card/sbi/
      cardOnboardURL: /card
      finalResponse_Url: /callback
      api_key_new:
      mle_ver: 1
      checkbin_New_Url: https://areionpg.pc.enstage-sas.com/binservice/v1/bins
    cscwallet:
      cancelurl: https://dev.epay.sbi/api/payments/v1/wallet/sbi/cscccallback
      sbiredirectdvurl: https://dev.epay.sbi/api/payments/v1/wallet/sbi/cscccallback
      keyvalue: messag
    paypal:
      authentication: https://api-m.sandbox.paypal.com/v1/oauth2/token
      create:
        orders: https://api-m.sandbox.paypal.com/v2/checkout/orders
      client_id: ABy9leIuwTWw_rBS4YHOwM_cpY5o5B6544H1LRqPEUm4idOUCwjxLtRYbrnzNrZ_vAJW55hyaMRNdBdv
      client_secret: EHOdoXAg2MTsqfmbzhLKUj9-EqL76Jt1Z1E0P0n7dL3EcCgLSTtcEgzGf0pkCHkRptOyyyjTaq-zygDF
      return_url: https://dev.epay.sbi/api/payments/v1/paypal/callback?
      cancel_url: https://dev.epay.sbi/api/payments/v1/paypal/callback?
      transaction-risk-api: https://api-m.sandbox.paypal.com/v1/risk/transaction-contexts/
      capture:
        orders: https://api-m.sandbox.paypal.com/v2/checkout/orders
      paymentsRedirectUrl: https://dev.epay.sbi/ui/channel/paypal/sbi
    testbank:
      post_url:

UPI:
  UPI_CLIENT_ID: SBIEPAY_MID_2.0
  SECRETKEY: f65e8f0a484d45babd33c10b4535ef66
  OATH_USERNAME: oauth2-api-merweb-SBI0000000032588
  OATH_PASSWORD: 05B6948CCFCA37A74B3DDDD15F9482040A998019ED67D2C77B4F5554DCB48B13
  UPI_SBI_PUBLIC_KEY_PATH: keys/SBI0000000032588_UAT_1224_PublicKey.asc
  EPAY_PVT_KEY_PATH: keys/0x1D883787-sec.asc
  PACKET_ENCRYPTION_KEY: 25dea54b392d9b24803d95e2df4d11d8
  OAUTH_TOKEN_URL: https://uatupionline.sbi/upi2/oauth/token
  VALIDATE_VPA_CHECK_URL: https://uatupionline.sbi/upi2/upi/web/v2.0/validateVPAWeb
  VPA_COLLECT_URL: https://uatupionline.sbi/upi2/upi/web/v2.0/meCollectInitiateWeb
  TXN_STATUS_ENQUIRY_URL: https://uatupionline.sbi/upi2/upi/web/v2.0/meTranStatusQueryWeb
  UPI_CALLBACK_URL: https://uat.sbiepay.sbi/secure/upiProcessingServlet
  UPICONFIG:
    URL: http://localhost:9098/admin/v1/merchant/upi/getUpiConfigDeatils
  INTENT_API_URL: https://uatupionline.sbi/upi2/upi/mandate/signVerifyIntent
  CONFIG_DEATILS_URL: http://localhost:9097/admin/v1/merchant/upi/getUpiConfigDeatils
  HANDSAKE_API_URL: https://uatupionline.sbi/upi2/upi/oauth2-web-handshake
  TXN_STATUS_ENQUIRY_API_URL:
  VPA_CHECK_API_URL:

UPI2:
  INTENT_API_URL: https://uatupionline.sbi/upi2/upi/mandate/generateQrIntent
  mode: '16'
  category: '02'

PG:
  UPI_MERCHANT_ID: SBI0000000032588

UPI_PVT_KEY_PWD: Uat@Sbiepay
UPI_category: '01'
UPI_intentMode: '05'
UPI_ivtoken: 2F70CBBDFAE8DBA95F46CEB68A970673
UPI_keyid: 10
UPI_mode: '05'
UPI_purpose: '00'
UPI_qrMedium: '06'
UPI_ver: '01'
UPI_cu: INR
UPI_tier: TIER1
UPI_integrationType: WEBAPI
UPI_panNo: DCPPR2936B
UPI_mebusstype: Proprietor
UPI_settleType: NET
UPI_requestUrl1: https://uat.epay.sbi/api/payments/v1/upi/sbi/callback
UPI_requestUrl2: https://uat.epay.sbi/api/payments/v1/upi/sbi/callback
UPI_merchantType: LARGE
UPI_merGenre: ONLINE
UPI_onboardingType: AGGREGATOR
UPI_upiQrVpa: testmerchant@sbi
UPI_businessName: TestMerchant
UPI_mccCode: '9399'

upiqr:
  private:
    key:
      path: keys/0x1D883787-sec.asc
      password: Uat@Sbiepay
  sbi:
    public:
      key:
        path: keys/SBI0000000032588_UAT_1224_PublicKey.asc

upi:
  upiGatewayConfigDetailsUrl: /merchant/gateway
  server:
    private:
      key:
        path: 0x1D883787-sec.asc
    public:
      key:
        path: SBI0000000032588_UAT_1224_PublicKey.asc

wibmo:
  client_jks_filename: keys/sbiepay_newpg_intl.jks
  client_jks_file_pwd: keystore
  client_alias_name: client_keypair
  client_alias_pwd: password
  server_pk_alias_name: wibmo_pk
  proxy:
    required: Y
  client_jks_filename_rupay: keys/sbiepay_newpg_rupay.jks
  client_jks_file_pwd_rupay: Wibmo@123
  client_alias_name_rupay: Wibmo3dss
  client_alias_pwd_rupay: Wibmo@123
  server_pk_alias_name_rupay: de95d081-ce9c-4af7-aff6-121ce2fe58e4
  client_jks_file_pwd_intl:
  client_alias_name_intl:
  client_alias_pwd_intl:
  server_pk_alias_name_intl:

cors:
  allowedOrigins: '*'
  origin: https://dev.epay.sbi,http://localhost:9095

security:
  whitelist:
    url: /webjars/,/actuator/,/swagger-resources/,/v3/api-docs,/swagger-ui/,/swagger-ui.html,/token,/downtime/api,/s1/fetch-data,/payments/v1/sbi/,/sbi/inb,/cards/sbi/**
    urls: /webjars/,/actuator/,/swagger-resources/,/v3/api-docs,/swagger-ui/,/swagger-ui.html,/token,/downtime/api,/s1/fetch-data,/payments/v1/sbi/,/sbi/inb,/cards/sbi/**
  endpoints: /webjars/,/actuator/,/swagger-resources/,/v3/api-docs,/swagger-ui/,/swagger-ui.html,/token,/downtime/api,/s1/fetch-data,/payments/v1/**,/sbi/inb
  jwt:
    secret:
      key: gdjfgs kjfhsdjkhkflkdlksdlfkskfwperip3ke3le3lmldrnkfnhiewjfejfokepfkldkfoikfokork3dklwedlsvflvkfkv lkdfvodk vcdokro3
      issuer: sbi.epay
  cors:
    origin: https://dev.epay.sbi,http://localhost:9095
    allowed:
      origins: http://localhost:9095,https://dev.epay.sbi
      methods: GET, POST
      headers: Authorization, Origin, X-Correlation-Id, Content-Type, Accept, Content-Disposition
      max-age: 3600

external:
  api:
    admin:
      services:
        base:
          path: http://admin-adminservice.dev-admin.svc.cluster.local:9094/api/admin/v1
    transaction:
      services:
        base:
          path: http://txn-transactionservice.dev-transaction.svc.cluster.local:9092/api/txn/v1
    ui:
      service:
        redirectView: https://dev.epay.sbi/ui/channel/sbi?
    paymentCallBackUrl: https://dev.epay.sbi/demo/
    sms:
      gateway:
        base:
          path: https://smsapiprod.sbi.co.in:9443
        url: /bmg/sms/epaypgotpdom
        user: epaypgotpdom
        password: Ep@y1Dpt
      body:
        content:
          type: text
        sender:
          id: SBIBNK
        int:
          flag: 0
        charging: 0

kms:
  service:
    base-url: https://dev.epay.sbi/api/kms/v1
    cors-origin: https://dev.epay.sbi

key:
  aek: BiIZ5feKr16Td3XSpVyqwXlwRNfSy9Gtis04WqEbD/0=

email:
  recipient: ebms_uat_receiver@ebmsgits.sbi.co.in
  from: ebms_uat_sender@ebmsgits.sbi.co.in

gateway:
  pooling:
    kafka:
      sslConfig:
        provided: yes

request:
  ServicePoint:
    ConnectionLimit: 12

cashchallan:
  api:
    eis:
      services:
        publickey:
          path:
        privatekey:
          path:
        gateway:
          enquiry: https://eissiuat.sbi.co.in/gen5/gateway/payments/Dr1Cr2MR/enquiry
          branchcode: '05049'
          sourceid: NY
          sbisourceid: SBINY
    maxlength:
      otherdetails: 0

aws:
  s3:
    key: IDHJO1513FFMMNLPR9BC
    secret: avXqEPv5B_QqqPK0D1VJzP3pSyAA4x31Zu_KucQ9
    region: ap-south-1
    url: https://s3store.bank.sbi/
    bucket:
      report: epay-nonprod-s3bucket
      ops: ${aws.s3.bucket.report}

neft:
  kafka:
    outbound:
      topic: neft.outbound.kafka.topic
    inbound:
      topic: neft.inbound.kafka.topic
  pdf:
    challan:
      accountnumber: AGG
      beneficiaryname: SBIePAY NEFT
      branchname: FINANCIAL INSTITUTIONS BRANCH
      ifsccode: SBIN0011777

rtgs:
  kafka:
    outbound:
      topic: rtgs.outbound.kafka.topic
    inbound:
      topic: rtgs.inbound.kafka.topic

neft.mis.outbound.kafka.topic: neft.mis.outbound.kafka.topic
neft.mis.inbound.kafka.topic: neft.mis.inbound.kafka.topic
rtgs.mis.inbound.kafka.topic: rtgs.mis.inbound.kafka.topic
rtgs.mis.outbound.kafka.topic: rtgs.mis.outbound.kafka.topic

scheduler:
  cron:
    expression:
      paypal-token: '0 */5 * * * *'
  time:
    zone: Asia/Kolkata
  paypal-token:
    lockAtLeastFor: PT30S
    lockAtMostFor: PT4M

standard:
  mid-list: '1000857'

challan:
  pdf:
    regeneration:
      link:
