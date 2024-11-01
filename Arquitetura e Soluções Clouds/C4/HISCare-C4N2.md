C4Container
    title Diagrama de Container do HISCare

    Enterprise_Boundary(b0, "HISCare"){

        System_Boundary(b1, "Usuários"){
            Person(paciente, "Paciente", "Registra Informações de Saúde e entra em contato com o médico")
            Person(medico, "Médico", "Visualiza seus pacientes")
        }

        System_Boundary(b2, "Sistema Interno") {
            Container(web_app, "Aplicação Web", "Node.JS, React", "Interface web para pacientes e médicos")
            Container(api, "API", "Node.js, Express", "API RESTful para comunicação entre front-end e back-end")
            Container(db, "Banco de Dados", "PostgreSQL", "Armazena informações de pacientes, agendamentos e prontuários")
        }

        System_Boundary(b3, "Sistena Externo"){
            System_Ext(auth, "Serviço de Autenticação", "Plataformas como Facebook ou Google <br/> que fornecem login social")
            System_Ext(email, "Sistema de Email", "Envia lembretes aos pacientes <br> e notifica médico e paciente sobre consultuas futuras")
        }
    }  

    Rel(paciente, web_app, "Usa", "HTTPS")
    Rel(medico, web_app, "Usa", "HTTPS")
    Rel(web_app, api, "Faz requisições para", "HTTPS")
    Rel(api, db, "", "SQL")
    Rel(api, auth, "", "HTTPS")
    Rel(api, email, "Manda Email <br>Usando")
    Rel(email,paciente,"Manda email para")
    Rel(email,medico,"Manda email para")

    UpdateLayoutConfig($c4ShapeInRow="8", $c4BoundaryInRow="1")
    UpdateRelStyle("web_app", "api", $offsetY="35", $offsetX="-50")
    UpdateRelStyle("api", "email", $offsetY="-60", $offsetX="-85")
    UpdateRelStyle("email", "medico", $offsetY="80", $offsetX="5")
    UpdateRelStyle("email", "paciente", $offsetY="280", $offsetX="50")
