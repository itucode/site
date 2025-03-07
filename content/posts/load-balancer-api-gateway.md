---
title: "Load Balancer: Antes ou Depois do API Gateway?"
date: 2025-03-05T12:00:00
author: "Seu Nome"
tags: ["arquitetura", "system design", "infraestrutura"]
categories: ["System Design", "Arquitetura"]
draft: false
summary: "Onde posicionar um Load Balancer na arquitetura de um sistema? Antes ou depois de um API Gateway? Essa decisão impacta escalabilidade, segurança e desempenho. Neste post, exploramos os cenários mais comuns e as melhores práticas para garantir uma arquitetura eficiente e resiliente."
---

Ao projetar uma arquitetura escalável para aplicações modernas, uma dúvida comum surge: **onde colocar o Load Balancer?** Ele deve ficar **antes** do API Gateway ou **depois**? Essa decisão afeta diretamente a escalabilidade, segurança e resiliência da aplicação.

## Load Balancer Antes do API Gateway

Colocar um Load Balancer **antes** do API Gateway significa distribuir o tráfego entre várias instâncias do API Gateway. Esse modelo tem algumas vantagens:

✅ **Alta disponibilidade**: Se um API Gateway falhar, o Load Balancer direciona o tráfego para outra instância saudável.  
✅ **Escalabilidade**: Permite escalar o API Gateway horizontalmente.  
✅ **Proteção contra picos de tráfego**: O Load Balancer distribui melhor as conexões.

No entanto, há também algumas desvantagens:

❌ **Maior complexidade**: Requer monitoramento e configuração adequada das instâncias do API Gateway.  
❌ **Latência adicional**: Cada requisição passa por mais um nível de roteamento.

### Quando usar essa abordagem?

- Quando há múltiplas instâncias do API Gateway para balancear carga.
- Quando o API Gateway precisa ser altamente disponível.
- Quando há necessidade de gerenciar falhas em gateways específicos.

---

## Load Balancer Depois do API Gateway

Neste modelo, o API Gateway recebe todas as requisições diretamente e apenas depois as encaminha para um Load Balancer, que distribui as requisições entre as instâncias de backend (microservices, por exemplo).

✅ **Controle centralizado**: O API Gateway pode aplicar regras de roteamento, autenticação e rate limiting antes do Load Balancer.  
✅ **Maior segurança**: Todas as requisições passam pelo API Gateway antes de serem balanceadas.  
✅ **Melhor gerenciamento de políticas**: Facilita a aplicação de regras de segurança e roteamento por serviço.

Mas há algumas desvantagens:

❌ **Menor resiliência**: Se o API Gateway falhar, todo o tráfego é interrompido.  
❌ **Pode ser um gargalo**: O API Gateway pode se tornar um único ponto de falha ou limitação de desempenho.

### Quando usar essa abordagem?

- Quando há regras de autenticação, autorização e rate limiting antes da distribuição de carga.
- Quando a prioridade é segurança e controle centralizado de APIs.
- Quando há um único API Gateway gerenciando todas as requisições.

---

## Qual é a Melhor Opção?

A escolha depende do contexto da aplicação. Aqui está um resumo:

| Abordagem                               | Vantagens                                                  | Desvantagens                                 |
| --------------------------------------- | ---------------------------------------------------------- | -------------------------------------------- |
| **Load Balancer antes do API Gateway**  | Melhor escalabilidade do API Gateway, alta disponibilidade | Mais complexo, pode aumentar latência        |
| **Load Balancer depois do API Gateway** | Segurança reforçada, controle centralizado                 | Menos resiliência, pode se tornar um gargalo |

Em arquiteturas distribuídas modernas, **uma abordagem híbrida pode ser usada**, onde um Load Balancer gerencia múltiplos API Gateways e cada API Gateway tem um Load Balancer para distribuir chamadas entre microservices.

## Conclusão

Se o objetivo é **escalar o API Gateway**, coloque o Load Balancer **antes**.  
Se a prioridade for **segurança e controle de requisições**, coloque o Load Balancer **depois**.

Em muitos casos, arquiteturas combinadas são ideais. O importante é avaliar as necessidades do sistema e garantir alta disponibilidade e performance.

---

Você já teve que decidir onde colocar um Load Balancer na sua arquitetura? Deixe seu comentário abaixo e compartilhe sua experiência!
