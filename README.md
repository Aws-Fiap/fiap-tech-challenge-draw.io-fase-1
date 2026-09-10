# Tech Challenge - Fase 1

Repositório com os diagramas de arquitetura AWS da Fase 1 do Tech Challenge (Pós-Tech FIAP), modelados em [draw.io](https://www.diagrams.net/).

## Conteúdo

| Arquivo | Descrição |
|---|---|
| `togglemaster-aws-architecture - Diagrama 1.drawio` | Diagrama da arquitetura com 2 páginas: versão **Horizontal** e versão **Vertical**. |
| `togglemaster-aws-architecture - Diagrama 2.drawio` | Variação do diagrama (layout Horizontal), incluindo legenda de portas e regras de tráfego. |

## Arquitetura

Os diagramas representam uma arquitetura básica de infraestrutura na AWS, contendo:

- **Região** `us-east-1`
- **VPC** contendo:
  - **Subnet pública**, com instância **EC2** protegida por Security Group liberando as portas `22` (SSH), `80` (HTTP) e `443` (HTTPS) para `0.0.0.0/0`
  - **Subnet privada**, com instância **RDS** (MySQL, porta `3306`), acessível apenas pela Security Group da subnet pública
- **Internet Gateway**, conectando a VPC à internet
- **Usuários** acessando a aplicação via Internet Gateway → EC2 (portas 80/443) → RDS (porta 3306)

## Como visualizar/editar

Os arquivos `.drawio` podem ser abertos de três formas:

1. **Online**: acesse [app.diagrams.net](https://app.diagrams.net/) e abra o arquivo desejado (`File > Open From > Device`).
2. **Desktop**: instale o [draw.io Desktop](https://github.com/jgraph/drawio-desktop/releases) e abra o arquivo diretamente.
3. **VS Code**: instale a extensão [Draw.io Integration](https://marketplace.visualstudio.com/items?itemName=hediet.vscode-drawio) e abra o `.drawio` no editor.

## GitHub Actions

O workflow [`export-diagrams.yml`](.github/workflows/export-diagrams.yml) exporta automaticamente todos os `.drawio` para PNG:

- Em **push** na `master` que altere algum `.drawio`: as imagens são geradas na pasta `exports/` e commitadas de volta no repositório.
- Em **pull requests** que alterem algum `.drawio`: as imagens são geradas e disponibilizadas como artifact do workflow (sem commit), para facilitar a revisão visual do diagrama no PR.
- Também pode ser disparado manualmente pela aba *Actions* (`workflow_dispatch`).

## Autores

Projeto desenvolvido para o Tech Challenge da Pós-Tech FIAP.
