 ```mermaid
   C4Component
   title Diagrama de Componentes do HISCare

   Container(mobileApp, "Aplicativo Mobile")
   Container(aplicacaoWeb, "Página Web")

   Boundary(b0, "Backend") {
      Component(sistemaPontuario, "Controlador de Login", "Responsável por lidar com os pedidos de conexões ao sistema.")
      Component(apiInforma, "Controlador de Dados das contas", "Disponibiliza os dados a serem usados na aplicação")
      Component(apiNoti, "Componente de Notificações", "Envia notificações para o usuário")
      Component(apiSeguranca, "Componente de Segurança", "Disponibiliza as funcionalidades relacionadas a login, trocar senha, etc.")
      Component(sistemaCalendario, "APIConsultas", "Um sistema que armazena todas as consultas realizadas e agendadas.")
   }
   Boundary(b1, "Bancos de Dados") {
      ComponentDb(SystemE, "Banco de Dados dos Pacientes", "MongoDB", "Armazena os dados de todos os pacientes que frequentam o Hospital.")
      ComponentDb(SystemC, "Banco de Dados dos Médicos", "MSQL Server", "Armazena os dados de todos os atuais e ex-funcionários do Hospital.")
   }
   Rel(aplicacaoWeb, sistemaPontuario, "Chama API")
   Rel(mobileApp, sistemaPontuario, "Chama API")
   Rel(aplicacaoWeb, sistemaCalendario, "Chama API")
   Rel(mobileApp, sistemaCalendario, "Chama API")
   Rel(aplicacaoWeb, apiInforma, "Chama API")
   Rel(mobileApp, apiInforma, "Chama API")
   Rel(sistemaPontuario, apiSeguranca, "Utiliza")
   Rel(sistemaCalendario, apiNoti, "Utiliza")
   Rel(apiSeguranca, SystemC, "Lê/Escreve")
   Rel(apiInforma, SystemE, "Lê/Escreve")
   ```