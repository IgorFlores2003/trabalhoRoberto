---
marp: true
theme: bespoke
class: lead
paginate: true
backgroundColor: #f7f7f7
backgroundImage: 'url(https://i.pinimg.com/originals/76/a6/5a/76a65a926d6276eaca577d4d1a22bfb5.jpg)'
---

<style>
  h1, h2 {
    color: #EF8E1E;
    margin-top: 0;
  }
  p, li {
    color: #FFFFFF;
    font-size: 27px;
    margin-top: 0;
    margin-bottom: 20px;
  }
  code {
    
    padding: 2px 4px;
    border-radius: 4px;
  }
</style>

# O Que é Instrumentação em Sistemas Distribuídos?

Instrumentação em sistemas distribuídos é o processo de adicionar pontos de medição para coletar dados sobre o comportamento e desempenho do sistema, similar à utilização de sensores em um veículo.

---

# Analogia com Veículos

- **Semelhança:** Assim como sensores em um carro monitoram a velocidade e o nível de combustível, a instrumentação em sistemas de TI captura métricas críticas de operação.
- **Importância:** Fundamental para monitorar e otimizar a operação em ambientes distribuídos e complexos.

---

# Por Que Instrumentar?

- **Visibilidade:** Facilita a visualização do desempenho do sistema em tempo real.
- **Diagnóstico rápido:** Permite identificar rapidamente a origem de falhas ou problemas de desempenho.
- **Otimização contínua:** Ajuda a melhorar a eficiência e reduzir custos ao identificar gargalos.

---

# Benefícios da Instrumentação

1. **Monitoramento em tempo real:** Dashboards atualizados com indicadores vitais do sistema.
2. **Diagnóstico de problemas:** Facilidade para rastrear problemas reportados por usuários.
3. **Otimização de desempenho:** Identificação de gargalos e pontos de ineficiência.
4. **Previsão de problemas:** Capacidade de antecipar falhas antes que impactem significativamente os usuários.
   

---

# Exemplo Prático: Amazon

- **Front-end:** Monitoramento de interações do usuário e performance da interface.
- **Back-end:** Análise de resposta dos serviços de recomendação e bancos de dados.
- **Rede:** Avaliação de latência e estabilidade da conexão.

---

```java
public GetProductInfoResponse getProductInfo(GetProductInfoRequest 
request) { 
 
  // check our local cache 
  ProductInfo info = localCache.get(request.getProductId()); 
   
  // check the remote cache if we didn't find it in the local cache 
  if (info == null) { 
    info = remoteCache.get(request.getProductId()); 
  
 localCache.put(info); 
  } 
   
  // finally check the database if we didn't have it in either cache 
  if (info == null) { 
    info = db.query(request.getProductId()); 
  
 localCache.put(info); 
 remoteCache.put(info); 
  } 
   
  return info; 
}

```
# Exemplo Prático: Amazon

---


```java
public GetProductInfoResponse getProductInfo(GetProductInfoRequest 
request) { 
 
  // Which product are we looking up? 
  // Who called the API? What product category is this in? 
 
  // Did we find the item in the local cache? 
  ProductInfo info = localCache.get(request.getProductId()); 
   
  if (info == null) { 
    // Was the item in the remote cache? 
    // How long did it take to read from the remote cache? 
    // How long did it take to deserialize the object from the cache? 
    info = remoteCache.get(request.getProductId()); 
  
    // How full is the local cache? 
    localCache.put(info); 
  } 
   
Instrumentando sistemas distribuídos para visibilidade operacional 
// finally check the database if we didn't have it in either cache 
if (info == null) { 
// How long did the database query take? 
// Did the query succeed?  
// If it failed, is it because it timed out? Or was it an invalid 
query? Did we lose our database connection? 
// If it timed out, was our connection pool full? Did we fail to 
connect to the database? Or was it just slow to respond? 
info = db.query(request.getProductId()); 
// How long did populating the caches take?  
// Were they full and did they evict other items?  
localCache.put(info); 
remoteCache.put(info); 
} 
// How big was this product info object?  
return info; 
} 

```
# Exemplo Prático: Amazon
---

# Definições e Conceitos Expandidos

- **Instrumentação detalhada:** Implementação de código e ferramentas para o monitoramento contínuo de latência, tráfego de rede, uso de recursos e falhas.

---

# Funcionamento Detalhado

- **Agentes de software:** Incorporados ao código da aplicação para registrar eventos e métricas.
- **Ferramentas externas:** Monitoram a infraestrutura sobre a qual as aplicações operam.

---

# Casos de Uso Detalhados

1. **Gerenciamento de performance**
2. **Monitoramento de saúde do sistema**
3. **Análise de segurança**
4. **Cumprimento de SLAs**

---

# Características da Instrumentação

- **Tempo real e histórico:** Análise instantânea e retrospectiva.
- **Granularidade ajustável:** Detalhamento conforme necessidade.
- **Extensibilidade:** Integração com outras ferramentas e sistemas.

---

# Vantagens e Desafios

**Vantagens:**
- **Proatividade:** Identificação precoce de problemas.
- **Otimização de recursos:** Uso eficiente, redução de custos.

**Desafios:**
- **Complexidade técnica:** Implementação e manutenção complexas.
- **Impacto no desempenho:** Potencial degradação se mal projetada.

---

# Conclusão

A instrumentação é essencial, atuando como o sistema nervoso de aplicações distribuídas, crucial para diagnósticos precisos e otimização contínua.
