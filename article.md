# Azure Open AI na VNet

## Introdução
Modelos GPT estão hospedados em vários fornecedores de serviços no momento, e o Microsoft Azure é um deles. Embora os modelos em si sejam os mesmos, existem muitas diferenças, incluindo:
- custo
- funcionalidades
- tipo de modelos e versões
- localização geográfica
- segurança
- suporte
- etc.

Um dos aspectos mais importantes ao usá-lo em um ambiente corporativo é, claro, a segurança. Ao utilizar os recursos de segurança da rede Azure com o Azure Open AI, os clientes podem consumir o serviço Open AI a partir e dentro da VNet, portanto, nenhuma informação está fluindo em público.

## Implantação de Exemplo
O repositório de amostras do Azure fornece arquivos bicep de exemplo para implantar o Azure Open AI em um ambiente VNet.
GitHub: openai-enterprise-iac

### Principais Recursos
Os principais recursos utilizados pelo bicep são:
- VNet
- Integração de VNet para Web App
- Endpoint Privado para Azure Open AI
- Endpoint Privado para Pesquisa Cognitiva
- Zona DNS Privada

Ao usar esses recursos, todo o tráfego de saída do Web App é roteado apenas dentro da VNet e todos os nomes são resolvidos em endereços IP privados. Open AI e Pesquisa Cognitiva desativam o endereço IP público, assim não há mais um endpoint de interface pública disponível.

## Implantar
O arquivo bicep implantará os seguintes recursos do Azure.
Vamos implantar e confirmar como funciona. Criei um grupo de recursos na região East US para meu próprio teste.

```bash
git clone https://github.com/Azure-Samples/openai-enterprise-iac
cd openai-enterprise-iac
az group create -n openaitest -l eastus
az deployment group create -g openaitest -f .\infra\main.bicep
```

Uma vez que eu execute o comando acima, vejo que a implantação começou. Espere até que a implantação seja concluída.

## Teste
Vamos ver se a implantação foi bem-sucedida.

### Azure Open AI
Vamos tentar o acesso público primeiro. Eu consegui criar uma implantação sem problemas. Mas quando eu tento do Chat playground no meu portal Azure, vejo o seguinte erro.

E quanto ao acesso via API Web? De uma ferramenta avançada do App Service, eu faço login na sessão Bash e primeiro faço um ping na URL do serviço. Vejo que o endereço IP privado atribuído ao Endpoint Privado é retornado. Em seguida, uso o comando curl para enviar a solicitação ao endpoint.

## Conclusão
A integração do Azure Open AI em uma VNet oferece uma camada adicional de segurança, garantindo que as informações não sejam expostas publicamente. Isso é crucial para ambientes corporativos que lidam com dados sensíveis e requerem uma infraestrutura de segurança robusta.
# Azure Open AI na VNet

## Introdução
Modelos GPT estão hospedados em vários fornecedores de serviços no momento, e o Microsoft Azure é um deles. Embora os modelos em si sejam os mesmos, existem muitas diferenças, incluindo:
- custo
- funcionalidades
- tipo de modelos e versões
- localização geográfica
- segurança
- suporte
- etc.

Um dos aspectos mais importantes ao usá-lo em um ambiente corporativo é, claro, a segurança. Ao utilizar os recursos de segurança da rede Azure com o Azure Open AI, os clientes podem consumir o serviço Open AI a partir e dentro da VNet, portanto, nenhuma informação está fluindo em público.

## Implantação de Exemplo
O repositório de amostras do Azure fornece arquivos bicep de exemplo para implantar o Azure Open AI em um ambiente VNet.
GitHub: openai-enterprise-iac

### Principais Recursos
Os principais recursos utilizados pelo bicep são:
- VNet
- Integração de VNet para Web App
- Endpoint Privado para Azure Open AI
- Endpoint Privado para Pesquisa Cognitiva
- Zona DNS Privada

Ao usar esses recursos, todo o tráfego de saída do Web App é roteado apenas dentro da VNet e todos os nomes são resolvidos em endereços IP privados. Open AI e Pesquisa Cognitiva desativam o endereço IP público, assim não há mais um endpoint de interface pública disponível.

## Implantar
O arquivo bicep implantará os seguintes recursos do Azure.
Vamos implantar e confirmar como funciona. Criei um grupo de recursos na região East US para meu próprio teste.

```bash
git clone https://github.com/Azure-Samples/openai-enterprise-iac
cd openai-enterprise-iac
az group create -n openaitest -l eastus
az deployment group create -g openaitest -f .\infra\main.bicep
```

Uma vez que eu execute o comando acima, vejo que a implantação começou. Espere até que a implantação seja concluída.

## Teste
Vamos ver se a implantação foi bem-sucedida.

### Azure Open AI
Vamos tentar o acesso público primeiro. Eu consegui criar uma implantação sem problemas. Mas quando eu tento do Chat playground no meu portal Azure, vejo o seguinte erro.

E quanto ao acesso via API Web? De uma ferramenta avançada do App Service, eu faço login na sessão Bash e primeiro faço um ping na URL do serviço. Vejo que o endereço IP privado atribuído ao Endpoint Privado é retornado. Em seguida, uso o comando curl para enviar a solicitação ao endpoint.

## Conclusão
A integração do Azure Open AI em uma VNet oferece uma camada adicional de segurança, garantindo que as informações não sejam expostas publicamente. Isso é crucial para ambientes corporativos que lidam com dados sensíveis e requerem uma infraestrutura de segurança robusta.