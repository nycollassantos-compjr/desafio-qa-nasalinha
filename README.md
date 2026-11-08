# 🧪 NaSalinha: Auditoria de Qualidade (QA)

Portfólio de qualidade do **Desafio QA Comp Júnior 2026/2**. Este repositório reúne os casos de teste, os bug reports, a coleção de API e o relatório final da auditoria do projeto **NaSalinha**, um app de check-in gamificado.

## 🎯 Escopo
Auditoria das três áreas core:
1. **Autenticação JWT:** cadastro, login, verificação de conta, permissões por perfil e segurança de senha.
2. **Check-in por Foto:** upload, status, restrição de propriedade e armazenamento em nuvem.
3. **Pontuação e Ranking:** soma e subtração de pontos, ordenação e regra de intervalo entre check-ins.

## 🛠️ Tecnologias e ferramentas

**Sistema testado:** Node.js, Express, Prisma e PostgreSQL (backend); React 18 e Tailwind (frontend); Mailtrap (e-mail) e Cloudinary (imagens); Docker e Docker Compose.

**Ferramentas de QA:**
| Ferramenta | Uso |
|---|---|
| GitHub Projects | Kanban e casos de teste |
| GitHub Issues | Bug reports |
| Insomnia | Testes de API |
| Navegador (DevTools, F12) | Testes funcionais e inspeção de rede/armazenamento |
| Docker logs e `psql` | Logs do backend e conferência de dados no banco |

## 🎯 Tipos de testes aplicados
* **Testes Funcionais (Manual/UI):** validação das telas e fluxos de usuário.
* **Testes de API:** validação dos endpoints, contratos, payloads e Status Codes.
* **Testes de Regressão:** garantia de que correções de bugs não afetaram o sistema existente. Os três casos de regressão são **simulados**: descrevem os testes a repetir se a correção fosse implantada, sem execução.

## 🧭 Estratégia de testes
- **Planejamento antes da execução:** casos de teste escritos a partir dos requisitos (RF/RNF) das três áreas, com 2 casos por requisito (funcional e API), mais um caso de regressão por área.
- **Execução:** casos funcionais no navegador e de API no Insomnia, acompanhando os logs do Docker. Dados forjados no banco (por exemplo, datas de check-in) quando o cenário exige.
- **Documentação:** cada falha vira um bug report em Issues, ligado ao caso de teste de origem. Cenários descobertos fora do plano entram como casos **Ad-hoc**.
- **Severidade:** Crítica (trava o sistema), Maior (erro de lógica) e Menor (erro visual).

## 📂 Onde encontrar cada artefato
| Artefato | Local |
|---|---|
| Casos de teste e Kanban | [GitHub Projects](https://github.com/nycollassantos-compjr/desafio-qa-nasalinha/projects) |
| Bug reports | [Issues](https://github.com/nycollassantos-compjr/desafio-qa-nasalinha/issues) |
| Coleção de API (Insomnia) | [`/api/nasalinha-collection.json`](api/nasalinha-collection.json) |
| Relatório de Testes Final | [`RelatorioFinal.md`](RelatorioFinal.md) |

## 🚀 Como rodar o projeto testado
1. Clone o repositório do desafio: https://github.com/Gustavohmmagalhaes/nasalinha-qa-challenge.git.
2. As instruções estão no próprio repositório do desafio 

## 🧪 Como usar a coleção de API
1. Com o ambiente rodando e o seed aplicado, importe `api/nasalinha-collection.json` no Insomnia (Import).
2. Rode primeiro as requisições de **login** para gerar os tokens e atualize os valores de `token_*` no ambiente.
3. Os IDs de check-in e de usuários criados nos testes são do meu ambiente: gere os seus rodando antes as requisições de cadastro e de check-in, e atualize as variáveis.
4. Nos testes de upload (campo `photo`), selecione uma imagem local (jpg, png, gif ou webp, até 5 MB).

## 📊 Resultado resumido
[X] casos planejados, [X] executados, [X] Pass e [X] Fail. [9] bugs encontrados, todos de severidade **Maior**. Detalhes em [`RELATORIO.md`](RELATORIO.md).
