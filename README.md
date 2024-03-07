# Estudo Terraform para criar um bucket S3 na AWS e o fluxo de trabalho GitHub Actions para automatizar o processo de criação desse bucket.

## Pré-requisitos
- Uma conta na AWS com credenciais de acesso configuradas.
- Um repositório GitHub onde você deseja implementar essa automação.
- A IDE VSCO.


## No arquivo Terraform :
1. Declarar o provider , provider é tipo um plugin da terraform , então se por exemplo usar o provider da aws 
temos acesso ao diversos recursos dentro da aws

2. Declarar a variavel , para o codigo ser generico , para não precisar escrever diretamente 
o nome do bucket por exemplo , então ele recebe esse nome através de uma variavel 

3. Declarar o recurso , o resource é a parte mais importante do terraform , ele representa o objetos da infraestrutura
ou seja são as configurações que a gente faz na nossa infraestrutura, desde a criação de recursos provisonamento de recursos 
até a configuração de algum recurso que já existe , então por exemplo mudar as permissões daque recurso, trocar
a memoria , trocar a maquina etc .
  - Nesse codigo é um exemplo de codigo que está criando um bucket S3 com o nome static-site-${var.bucket_name} e configurando o website do bucket.

4. Definir bloqueios de acesso público, controles de propriedade e ACLs para o bucket.

## No arquivo yaml 
- O fluxo de trabalho GitHub Actions é acionado quando uma nova issue é aberta.
O fluxo de trabalho realiza as seguintes etapas:
  - Verifica o repositório.
  - Configura as credenciais da AWS.
  - Extrai o nome do bucket da issue aberta.
  - Executa o Terraform para criar o bucket S3 usando o nome extraído da issue.
  - Adiciona um comentário na issue aberta informando que o bucket S3 foi criado com sucesso.

## Configuração do GitHub Actions:

1. No seu repositório GitHub, crie um diretório chamado .github/workflows se ainda não existir.
2. Dentro deste diretório, crie um arquivo YAML para definir o fluxo de trabalho de automação. Você pode nomeá-lo como preferir. Por exemplo, terraform_workflow.yaml.
3. Cole o código YAML fornecido na seção "Fluxo de trabalho GitHub Actions" acima no arquivo que você criou.
4. Certifique-se de configurar as secrets AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY e GH_TOKEN em suas configurações de repositório no GitHub.

## Executando a Automação:

- Sempre que uma nova issue for aberta no seu repositório, o fluxo de trabalho será acionado automaticamente.
- Ele extrairá o nome do bucket da issue, criará o bucket S3 na AWS usando Terraform e adicionará um comentário na issue informando que o bucket foi criado com sucesso.
Verificação:

- Após a execução bem-sucedida do fluxo de trabalho, verifique sua conta AWS para confirmar se o bucket S3 foi criado com o nome correto.
- Verifique a issue no GitHub para confirmar se o comentário foi adicionado corretamente.

_________________________________
Fonte : https://www.youtube.com/watch?v=BslJdgv_I2c
