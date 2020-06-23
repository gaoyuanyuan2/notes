# Tomcat

Bootstrap

Connector->initInternal();  protocolHandler.init() ->AbstractHttp11Protocol  super.init()

->AbstractProtocol  endpoint.init(); -> AbstractEndpoint  init() > bind() 

AprEndpoint  Nio2Endpoint NioEndpoint 三种实现


![四种隔离级别](/img/43.jpg) 