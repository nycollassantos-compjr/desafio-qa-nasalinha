# Relatório de Testes Final: NaSalinha

## 1. Escopo
Auditoria de qualidade das três áreas core (Autenticação JWT, Check-in por Foto e Pontuação e Ranking), com testes funcionais (navegador), de API (Insomnia) e de regressão (simulada). Ambiente local com Docker. Casos de teste gerenciados no GitHub Projects e bugs no GitHub Issues.

## 2. Métricas de execução

| Área | Planejados | Executados | Pass | Fail | Não executados |
|---|---|---|---|---|---|
| Autenticação JWT | 9 | 8 | 5 | 3 | 1 |
| Check-in por Foto | 10 | 9 | 5 | 4 | 1 |
| Pontuação e Ranking | 8 | 7 | 3 | 4 | 1 |
| **Total** | **27** | **24** | **13** | **11** | **3** |

- Execução: 24 de 27 casos (88,9%).
- Sobre os executados: 13 Pass (54,2%) e 11 Fail (45,8%).
- Os 3 casos não executados são os de regressão, que são simulados: descrevem os testes a repetir caso a correção de um bug fosse implantada, e por isso não têm Pass/Fail.
- Inclui 1 caso Ad-hoc (CT-PTS-AD-HOC-01, rejeição de check-in aprovado sem redução de pontos).

## 3. Distribuição de severidade

| Severidade | Definição | Quantidade | % |
|---|---|---|---|
| Crítica | Trava o sistema | 0 | 0% |
| Maior | Causa erro de lógica | 9 | 100% |
| Menor | Erro visual | 0 | 0% |
| **Total de bugs** | | **9** | **100%** |

Status dos bugs: 9 abertos e 0 corrigidos. A classificação segue a escala do desafio: nenhum bug trava o sistema (Crítica) e nenhum é exclusivamente visual (Menor). Todos são falhas de regra de negócio no backend (Maior).

### Bugs por área

| Área | Bugs |
|---|---|
| Autenticação JWT | 2 |
| Check-in por Foto | 4 |
| Pontuação e Ranking | 3 |

## 4. Bugs encontrados

| Issue | Título | Área | Requisito | Caso de teste | Severidade |
|---|---|---|---|---|---|
| #1 | Fluxo de verificação de e-mail ausente | JWT | RF-01 | CT-JWT-01 | Maior |
| #5 | Usuário é criado sem o status PENDENTE e os tokens já são enviados no cadastro | JWT | RF-01, RF-02 | CT-JWT-02 | Maior |
| #2 | Check-in é criado com status APROVADO sem passar pela moderação do admin | Check-in | RF-05 | CT-CHK-03 | Maior |
| #3 | Usuário comum consegue visualizar check-ins de outros usuários | Check-in | RF-06 | CT-CHK-05 | Maior |
| #6 | Endpoint de check-in permite realizar múltiplos check-ins no mesmo dia | Check-in | RF-04 | CT-CHK-02 | Maior |
| #9 | Envio da mesma foto repetidas vezes é permitido | Check-in | RF-04 | CT-CHK-09 | Maior |
| #4 | Pontuação do usuário não é subtraída ao excluir um check-in | Pontuação | RF-08 | CT-PTS-03, CT-PTS-04 | Maior |
| #8 | O segundo check-in em menos de 24 horas é permitido | Pontuação | RF-09 | CT-PTS-06 | Maior |
| #7 | Mudança de status do check-in para Rejeitado não reflete na pontuação | Pontuação | RF-07 | CT-PTS-AD-HOC-01 (Ad-hoc) | Maior |

Algumas falhas de casos de teste compartilham a mesma causa (por exemplo, CT-PTS-03 e CT-PTS-04), por isso há menos bugs do que casos reprovados.

## 5. Estado atual da qualidade

O sistema apresenta falhas de regra de negócio nas três áreas, sem travar nenhum fluxo. Os riscos principais são:

- **Controle de acesso:** não há verificação de conta (contas são criadas sem status PENDENTE e já recebem tokens no cadastro), e usuários comuns conseguem visualizar check-ins de outros usuários.
- **Check-in:** as regras de um check-in por dia, de intervalo de 24 horas e de foto repetida não são aplicadas, e todo check-in nasce aprovado, sem moderação do Admin.
- **Pontuação:** o saldo do usuário só é calculado na criação do check-in. Excluir ou rejeitar um check-in não reduz os pontos, o que distorce o ranking.

Combinadas, essas falhas permitem acumular pontos sem validação de conta, de frequência ou de evidência. Recomenda-se corrigir primeiro o fluxo de verificação e as validações do endpoint de check-in, pois elas afetam as demais áreas.

## 6. Observações
- Testes de regressão simulados (CT-JWT-09, CT-CHK-10, CT-PTS-07), sem execução.
- A coleção de API exportada do Insomnia está no repositório.
