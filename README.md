# azure-car-rental-cloud-native.
Arquitetura Cloud-Native para locadora de veículos. Implementação de padrão BFF (Backend for Frontend) e processamento serverless com Azure Functions (RentProcess e Payment).

# 🚗 Sistema de Aluguel de Carros Cloud-Native na Azure

Este repositório documenta a arquitetura e o desenvolvimento de um sistema de gerenciamento de aluguel de carros baseado em nuvem (Cloud-Native), desenvolvido como projeto prático para o bootcamp da Digital Innovation One (DIO).

> **Nota de Arquitetura:** O projeto propõe uma solução escalável utilizando o padrão de microsserviços e computação serverless, separando as responsabilidades desde a camada de API até o processamento em background de aluguéis e pagamentos.

## 🎯 Objetivo do Projeto
Projetar e hospedar uma solução em nuvem completa para uma locadora de veículos. O foco é garantir que a aplicação seja resiliente, com componentes independentes que possam escalar conforme a demanda de reservas aumenta.

## 🏗️ Desenho da Solução e Componentes

A infraestrutura foi desenhada utilizando os seguintes serviços e padrões arquiteturais na Microsoft Azure:

1. **API BFF (Backend for Frontend):**
   * Uma camada de API dedicada a servir os dados exatos que a interface do usuário (aplicativo mobile ou web) precisa, sem expor a complexidade dos bancos de dados ou serviços internos.
2. **Azure Function - RentProcess:**
   * Serviço *serverless* acionado via gatilhos (Triggers) responsável por processar a lógica de negócio do aluguel: verificar disponibilidade de frota, registrar a reserva e atualizar o status do veículo.
3. **Azure Function - Payment:**
   * Microsserviço independente e seguro para lidar com a transação financeira. É acionado de forma assíncrona após a validação da reserva, garantindo que o sistema de aluguel não fique travado esperando a operadora de cartão.

## 💡 Insights e Aprendizados
* **Padrão BFF:** Aprendi como estruturar uma API BFF ajuda a reduzir o excesso de chamadas de rede (over-fetching) no lado do cliente, centralizando a orquestração no backend.
* **Desacoplamento com Serverless:** O uso de Azure Functions (`RentProcess` e `Payment`) demonstrou como separar processos críticos. Se o serviço de pagamento falhar ou sofrer instabilidade, o serviço de reserva de carros continua operando de forma independente.
* **Maturidade Cloud-Native:** O projeto consolida a visão de que aplicações modernas não dependem de grandes servidores monolíticos, mas sim de uma esteira de serviços gerenciados que escalam elásticamente.

## 🚀 Possibilidades de Evolução
Como melhoria contínua, esta arquitetura pode ser facilmente expandida integrando o **Azure API Management (APIM)** na frente do BFF para gerenciar limites de taxa (Rate Limit) e segurança, além de adicionar filas (Service Bus) para comunicação entre a function de Reserva e a de Pagamento.
