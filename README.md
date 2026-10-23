# Assistente de Investimentos com n8n

## Sobre o projeto

Workflow educativo criado no n8n para automatizar o tratamento de dados de clientes e preparar mensagens de e-mail com apoio de inteligência artificial.

O fluxo recebe clientes por Webhook, consulta um CSV de investimentos, processa os dados em JavaScript, seleciona uma opção de acordo com o perfil e saldo informado, pede à IA que prepare o texto do e-mail e valida o endereço antes do envio pelo Gmail.

## Nós do workflow

1. **Webhook** — recebe um pedido `POST` no caminho `Clientes`.
2. **HTTP Request** — consulta o CSV de investimentos disponibilizado no material do desafio.
3. **Code in JavaScript** — interpreta os dados CSV, incluindo campos entre aspas, e normaliza os valores mínimos.
4. **Merge** — combina os dados do Webhook e os investimentos.
5. **Code in JavaScript1** — compara perfil e saldo e prepara os resultados por cliente.
6. **Code in JavaScript2** — prepara os campos de todos os clientes, incluindo dados incompletos, para que possam ser tratados sem desaparecer silenciosamente do fluxo.
7. **Message a model** — gera um rascunho de e-mail sem promessas de ganhos ou garantias.
8. **Code in JavaScript3** — interpreta a resposta da IA e prepara o conteúdo do e-mail.
9. **If** — valida o formato do endereço de e-mail e confirma que existe uma recomendação antes de permitir o envio.
10. **Send a message** — envia o e-mail pelo Gmail quando o endereço passa na validação.
11. **Respond to Webhook** — devolve uma resposta genérica de conclusão pelo caminho de envio ou pelo caminho de endereço inválido.

## Como importar

1. Descarrega `assistente-investimentos-corrigido.json`.
2. Abre o n8n e importa o workflow a partir do ficheiro.
3. Configura as credenciais do modelo de IA e do Gmail na tua instância.
4. Confirma a URL do CSV e o formato do corpo do Webhook.
5. Testa primeiro com dados fictícios e com um endereço de e-mail que controles.

## Exemplo de dados de entrada

O código espera um objeto com uma lista `clientes`, por exemplo:

```json
{
  "clientes": [
    {
      "nome": "Cliente de Teste",
      "email": "teste@example.com",
      "perfil": "Conservador",
      "saldo": "R$ 1.500,00"
    }
  ]
}
```

Os valores de `perfil` devem corresponder aos perfis existentes no CSV. O exemplo é ilustrativo; confirma os nomes reais das colunas e os valores aceites no ficheiro de dados do desafio.

## Verificações importantes

- O CSV tem de ser devolvido como texto pelo nó HTTP Request.
- Confirma se os perfis dos clientes correspondem aos perfis do CSV.
- Testa endereços válidos e inválidos.
- Verifica as execuções no n8n antes de considerar o projeto concluído.
- A resposta do Webhook é genérica; não deve ser interpretada como prova de que todos os e-mails foram enviados com sucesso. Se o pedido contiver vários clientes e houver resultados nos dois ramos do nó If, testa cuidadosamente o comportamento da resposta HTTP, pois o Webhook só pode devolver uma resposta por pedido.
- As recomendações são uma demonstração técnica e não constituem aconselhamento financeiro.

## Segurança

O JSON partilhável foi preparado sem as referências de credenciais da instância original. Depois da importação, configura as credenciais no n8n. Nunca publiques tokens, palavras-passe, dados pessoais reais ou URLs privadas de Webhook.

## Tecnologias

- n8n
- JavaScript
- HTTP Request e Webhook
- Modelo de IA
- Gmail

## Autoria

Projeto educativo desenvolvido por Alda Benta no âmbito de desafios da DIO.
