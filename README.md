# Generic App Helm Chart

Este é um Helm chart genérico para deploy de aplicações containerizadas no Kubernetes. Ele usa o **nginx** como exemplo de imagem padrão, mas pode ser facilmente configurado para qualquer aplicação de contêiner.

## 📂 Estrutura do Chart

O chart contém os seguintes principais arquivos:

- **`values.yaml`**: Contém os valores padrão configuráveis para o chart.
- **`Chart.yaml`**: Metadados do Helm chart, incluindo nome, versão e descrição.
- **`templates/`**: Diretório contendo os recursos Kubernetes, como `Service` e `Deployment`.

## ⚙️ Parâmetros

Aqui estão os principais parâmetros que podem ser customizados via o arquivo `values.yaml`:

| Parâmetro                 | Descrição                                       | Valor Padrão    |
|---------------------------|-------------------------------------------------|-----------------|
| `replicaCount`            | Número de réplicas do Deployment                | `1`             |
| `image.repository`        | Repositório da imagem do container              | `nginx`         |
| `image.tag`               | Tag da imagem do container                      | `"1.16"`        |
| `image.pullPolicy`        | Política de pull da imagem                      | `IfNotPresent`  |
| `container.name`          | Nome do container dentro do pod                 | `app`           |
| `service.type`            | Tipo de serviço Kubernetes                      | `ClusterIP`     |
| `service.port`            | Porta exposta pelo serviço                      | `80`            |
| `resources.limits.cpu`    | Limite de CPU para o container                  | `"100m"`        |
| `resources.limits.memory` | Limite de memória para o container              | `"128Mi"`       |
| `resources.requests.cpu`  | CPU requisitada pelo container                  | `"50m"`         |
| `resources.requests.memory` | Memória requisitada pelo container            | `"64Mi"`        |

## 🚀 Como Instalar

### Instalar Diretamente do GitHub (Repositório Remoto)

Adicionar o repositório Helm (se ainda não tiver adicionado):

```bash
helm repo add generic-app https://owiltoncezar.github.io/generic-app/
```
Atualizar os repositórios Helm para garantir que você tenha a versão mais recente do repositório:

```bash
helm repo update
```
Instalar o chart remoto usando o nome desejado para a release e, se necessário, especificar o namespace:

```bash
helm install "seu-nome-de-release" generic-app/generic-app --namespace "nome-do-namespace" --create-namespace
```
Nota: Se você não especificar um namespace, ele será instalado no namespace padrão (default).

### Instalar a partir de uma Pasta Local

Para instalar localmente, você precisará clonar o repositório e depois usar o chart presente na pasta generic-app/. Siga os passos abaixo:

Primeiro, clone o repositório onde o Helm chart está armazenado:

```bash
git clone https://github.com/owiltoncezar/generic-app.git
```
Com o repositório clonado, você pode instalar o Helm chart diretamente do diretório generic-app/ usando o comando:

```bash
helm install "seu-nome-de-release" ./generic-app
```

**Notas:** 
 - Substitua "seu-nome-de-release" pelo nome desejado para sua instalação. Esse nome será usado como prefixo dos recursos criados no cluster.
 - O ./generic-app é o caminho para a pasta onde o seu chart está localizado. Certifique-se de que a pasta contém o arquivo Chart.yaml, values.yaml, templates/, etc.

Instalando em um namespace específico:

Se você quiser instalar o chart em um namespace específico, use a opção --namespace:

```bash
helm install "seu-nome-de-release" ./generic-app --namespace "nome-do-namespace"
```
Se o namespace ainda não existir, adicione a flag --create-namespace para criá-lo automaticamente:

```bash
helm install "seu-nome-de-release" ./generic-app --namespace "nome-do-namespace" --create-namespace
```

**Dica**: Se você não especificar um namespace, o Helm instalará os recursos no namespace padrão (default).

## 📌 Recursos Instalados

Este chart instala os seguintes recursos Kubernetes:

- **Service**: Um serviço `ClusterIP` expondo a aplicação na porta configurada.  
- **Deployment**: Um deployment para gerenciar os pods da aplicação, com as réplicas e configurações definidas.  

## 🎨 Customização
Você pode personalizar este chart ajustando o arquivo values.yaml ou usando parâmetros no comando helm install.

## 🔧 Exemplo de customização:
Para mudar a imagem do container, edite o values.yaml:

```yaml
image:
  repository: my-custom-app
  tag: "2.0"
  pullPolicy: Always
```  

## 📜 Licença
Este projeto está licenciado sob os termos da MIT License.
