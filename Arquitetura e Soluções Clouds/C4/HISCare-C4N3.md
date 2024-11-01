@startuml
!include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Component.puml
!define DEVICONS https://raw.githubusercontent.com/tupadr3/plantuml-icon-font-sprites/master/devicons
!define FONTAWESOME https://raw.githubusercontent.com/tupadr3/plantuml-icon-font-sprites/master/font-awesome-5
!include DEVICONS/msql_server.puml
!include DEVICONS/mongodb.puml


title Diagrama de Componentes do HISCare

Container(mobileApp, "Aplicativo Mobile")
Container(aplicacaoWeb, "Página Web")

Boundary(b0, "Backend"){
    Component(sistemaProntuario, "Controlador de Login", "Responsável por lidar com os pedidos de conexões ao sistema.")
    Component(apiInforma, "Controlador de Dados das contas", "Disponibiliza os dados a serem usados na aplicação")
    Component(apiNoti, "Componente de Notificações", "Envia notificações para o usuário")
    Component(apiSeguranca, "Componente de Segurança", "Disponibiliza as funcionalidades relacionadas a login, trocar senha, etc.")
    Component(sistemaCalendario, "APIConsultas", "Um sistema que armazena todas as consultas realizadas e agendadas.")
}


Boundary(b1, "Bancos de Dados") {
    ComponentDb(SystemE, "Banco de Dados dos Pacientes", "MongoDB", "Armazena os dados de todos os pacientes que frequentam o Hospital.", $sprite="mongodb")
    ComponentDb(SystemC, "Banco de Dados dos Médicos", "MSQL Server", "Armazena os dados de todos os atuais e ex-funcionários do Hospital.", $sprite="msql_server")
}


Lay_D(sistemaProntuario, apiSeguranca)
Lay_R(sistemaProntuario, apiInforma)
Lay_D(sistemaProntuario, apiNoti)
Lay_D(b0,b1)

Rel(aplicacaoWeb, sistemaProntuario, "Chama API")
Rel(mobileApp, sistemaProntuario, "Chama API")
Rel(aplicacaoWeb, sistemaCalendario, "Chama API")
Rel(mobileApp, sistemaCalendario, "Chama API")
Rel(aplicacaoWeb, apiInforma, "Chama API")
Rel(mobileApp, apiInforma, "Chama API")
Rel(sistemaProntuario, apiSeguranca, "Utiliza")
Rel(sistemaCalendario, apiNoti, "Utiliza")
Rel(apiSeguranca, b1, "Lê/Escreve")
Rel(apiInforma, b1, "Lê/Escreve")




SHOW_LEGEND()
@enduml