# Dicas para o Teste - BCB

Este documento contém dicas e melhores práticas para ajudá-lo a ter sucesso no teste BCB.

## Etapas do Desenvolvimento

Para organizar seu trabalho, sugerimos dividir o desenvolvimento nas seguintes etapas:

1. **Configuração inicial** - Setup do projeto, Docker, banco de dados
2. **Implementação do core** - Funcionalidades básicas de autenticação, clientes e mensagens
3. **Desenvolvimento do desafio principal** - Fila/priorização ou dashboard, conforme seu perfil
4. **Refinamentos e extras** - Se houver tempo, implemente funcionalidades bônus

## Importante Sobre o Tempo

- Este teste foi projetado para ser flexível, permitindo implementações de diferentes complexidades
- Se tiver apenas 1 dia: concentre-se na **Parte 1** para seu perfil e documente bem
- Se tiver 2-3 dias: tente avançar para as partes mais complexas conforme sua experiência
- **Lembre-se**: preferimos qualidade sobre quantidade

## Dicas para o Sucesso

### Planejamento
- Leia toda a documentação antes de começar
- Faça um esboço da arquitetura e dos componentes principais
- Defina as entidades e relacionamentos do banco de dados
- Priorize as funcionalidades essenciais

### Implementação
- Comece com uma versão mínima funcional antes de adicionar recursos avançados
- Mantenha o código limpo e organizado desde o início
- Implemente uma funcionalidade por vez, testando cada passo
- Use padrões de design adequados à linguagem/framework escolhido

### Entrega
- Documente suas decisões, especialmente limitações de tempo ou escolhas de design
- Use o README para explicar o que foi implementado e o que ficou como trabalho futuro
- Garanta que o docker-compose funcione corretamente em um ambiente limpo
- Verifique se todas as dependências estão declaradas corretamente

### Diferenciais
- Adicione testes automatizados para as funcionalidades críticas
- Documente sua API (Swagger/OpenAPI)
- Implemente logs e monitoramento básico
- Considere aspectos de segurança e performance

## FAQ - Perguntas Frequentes

### Geral

**P: Preciso implementar todas as partes do desafio?**  
R: Não, implemente até onde conseguir com qualidade. Cada parte representa um nível de complexidade, e uma boa implementação da Parte 1 já é suficiente para avaliação.

**P: Posso usar bibliotecas e frameworks?**  
R: Sim, incentivamos o uso de bibliotecas e frameworks apropriados. Apenas documente as escolhas no README.

**P: Preciso implementar autenticação com JWT, OAuth, etc?**  
R: Não é necessário um sistema sofisticado. Uma autenticação simples baseada em token/header é suficiente.

**P: Como deve ser a persistência dos dados?**  
R: Para backend/fullstack, recomendamos um banco de dados real (PostgreSQL, MongoDB), mas para implementações mais simples, armazenamento em memória é aceitável.

### Backend

**P: Como deve funcionar exatamente a fila de mensagens?**  
R: Na implementação mais simples, pode ser um array em memória. Na versão mais completa, um sistema que processa mensagens considerando prioridade e ordem de chegada.

**P: A fila precisa ser persistente (sobreviver a reinicializações)?**  
R: Não é requisito obrigatório, mas seria um diferencial.

**P: O worker assíncrono precisa ser um processo/thread separado?**  
R: Idealmente sim, mas implementações mais simples como um loop em background também são aceitáveis.

**P: Preciso implementar um sistema real de envio de mensagens?**  
R: Não, basta simular o envio (ex: log, atualização de status, delay).

### Frontend

**P: Preciso implementar autenticação real?**  
R: Não, pode ser uma simulação. O importante é ter a tela de login e armazenar algum estado de sessão.

**P: É obrigatório fazer um design responsivo completo?**  
R: Espera-se pelo menos um layout que funcione razoavelmente em mobile e desktop, sem necessidade de design sofisticado.

**P: Posso usar bibliotecas de componentes UI prontos?**  
R: Sim, incentivamos o uso de bibliotecas como Material-UI, Bootstrap, Chakra, etc.

**P: Os dados mockados precisam ser extensos?**  
R: Não, é suficiente ter dados básicos para demonstrar as funcionalidades.

### Fullstack

**P: Devo focar mais no backend ou no frontend?**  
R: O ideal é um equilíbrio (40% backend, 40% frontend, 20% integração), mas você pode dedicar um pouco mais de tempo à parte em que tem mais experiência.

**P: É necessário usar Docker para o projeto fullstack?**  
R: Recomendamos fortemente, mas não é obrigatório se você fornecer instruções claras de como executar o projeto localmente.

**P: Posso simplificar partes do backend ou frontend?**  
R: Sim, o importante é ter um fluxo completo funcionando. Simplifique onde necessário, mas documente suas decisões.

## Lembre-se

- Não se preocupe em implementar tudo - queremos ver seu raciocínio e abordagem
- É melhor ter um subconjunto de funcionalidades bem implementadas do que tudo incompleto
- Estamos avaliando mais sua capacidade de resolver problemas do que a quantidade de código
- No live-coding, você terá oportunidade de explicar suas escolhas e mostrar seu raciocínio

**Boa sorte!**