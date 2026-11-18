# Arquitetura — AnanimCloudReport

Diagrama lógico, sem endereços, credenciais ou topologia de clientes.

```mermaid
flowchart LR
  A[APIs de provedores cloud] --> B[Coleta no backend]
  B --> C[Normalização por conta e projeto]
  C --> D[Cache e histórico JSON]
  D --> E[API Express]
  E --> F[Interface React]
  E --> G[Relatórios e exportações]
  E --> H[Inventário para Ananim NOC]
```

## Integração com provedores

O diagrama expressa a arquitetura lógica do produto. A entrada pode ser adaptada a provedores distintos por conectores que traduzam faturamento e inventário para uma análise comum. Isso não pressupõe que todas as APIs tenham o mesmo modelo ou que todos os conectores já existam. A versão documentada possui integração evidenciada com Huawei Cloud.

A camada de FinOps organiza conta, projeto, recurso e período para relacionar custo, consumo e responsabilidade. Novos conectores precisam validar moeda, descontos, impostos, granularidade e atualização antes de permitir comparações financeiras.

## Decisões de engenharia

### Coleta no backend

Concentra autenticação e integração; credenciais não pertencem à apresentação pública.

### Cache de resultados

Evita repetir chamadas caras em cada navegação e permite acompanhar a atualização. A interface precisa distinguir dado recente de coleta atrasada.

### Critério financeiro configurável

Valores brutos e ajustes comerciais precisam ter significado explícito. Percentuais e valores de clientes não são divulgados neste portfólio.

### Persistência em arquivos

Mantém a operação simples, mas exige atenção a escrita concorrente, consistência, backup e evolução do volume.

## Validação e operação

A validação de mudanças deve distinguir sintaxe/build, testes isolados, publicação e comportamento real. Um processo iniciado, uma resposta HTTP ou um botão habilitado não comprovam, isoladamente, o resultado esperado. Os detalhes operacionais, credenciais e registros de clientes ficam fora deste repositório.

## Fronteiras de responsabilidade

- A proposta atende provedores de cloud em geral por meio de integrações específicas. A cobertura depende do conector e dos dados disponibilizados por cada provedor; a integração evidenciada nesta versão é Huawei Cloud.
- Estimativas e oportunidades não equivalem a economia realizada ou garantida.
- Inventário, cobrança e estado operacional podem ter instantes de atualização diferentes.
- Relatórios não substituem validação da fatura, contrato de licenciamento ou teste de restauração.
