
# JARVIS MODULO ESP32 ROOT
  

## CONFIGURAÇÕES
- ID: ID do módulo no projeto JARVIS  (DEVE SER SEMPRE 1 para o Node ROOT)  
- STATION_SSID: nome da rede wifi  
- STATION_PASSWORD: senha da rede wifi  
- STATION_CHANNEL: canal do AP (necessário configurar o AP local para canal fixo)  
- jarvisHub: IP do Modulo HUB no projeto Jarvis

## FUNÇÕES
getMessageSensors(JsonDocument doc) - popula o JSON com as leituras dos sensores recebidas
getMessageHello(JsonDocument myObject); imprime as msg hello recebidas  
sendMessageHello(); envia msg hello a cada 11s  
checkConnection(); reinicia o ESP se perder conexao a rede mesh  
checkConnectionRoot(); testa a conexao do Node Root a rede Wifi a cada 20s, reinicia o ESP após 6 tentativas se perder acesso a rede WIFI ou conexao ao Modulo Jarvis Hub  
printRedeMesh(); imprime na tela o layout da rede mesh  
sendInfoIPConnectionRoot();  testa conexao ao Modulo Jarvis Hub  
IPAddress getlocalIP(); obtem o IP local do Node Root  

receivedCallback(uint32_t from, String &msg) -
    - 100 - msg hello
    - 200 - leitura de sensores

webServerEnable() - 
    / - retorna informações do Node Root - {"id":1,"description":"node root","ip":"192.168.1.2"} - usado para verificar se o node está online  
    /getModules - retorna os Modulos Online - {"16":"true"} - populado pela funcao getMessageHello, deve ser chamado com time acima de 11s  
    /getSensors - retorna a leitura dos sensores - {"1005":{"code":200,"idSensor":1005,"description":"nivel de agua da caixa dagua","cheio":false,"Meio":false,"vazio":false}} - populado pela funcao getMessageSensors(JsonDocument doc), deve ser chamado com time acima de 05s  

## Observações:
- Somente um dispositivo pode ser o nó raiz na malha (root)  
- Configurar o SSID e Senha da Rede WIFI Local
- Configurar Roteador WIFI para canal Manual, o mesmo canal do AP deve ser configurado em todos os dispositivos pertencentes a rede mesh

## Referências
https://github.com/jackson-veloso/ESP32_WATCHDOG
https://github.com/jackson-veloso/ESP32_REDE_MESH_PAINLESSMESH

https://blog.eletrogate.com/criando-uma-rede-mesh-com-os-modulos-esp-8266-esp-32-esp-01/  
https://randomnerdtutorials.com/esp-mesh-esp32-esp8266-painlessmesh/  
https://gitlab.com/painlessMesh/painlessMesh  
https://www.fernandok.com/2018/06/travou-e-agora.html  
https://labdegaragem.com/forum/topics/esp32-travou-e-agora  
