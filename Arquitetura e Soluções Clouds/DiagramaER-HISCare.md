@startuml

entity UsuarioPaciente{
    *id : <<generated>>
    nome : string
    email : string
    age : date
    sexo : string
    altura : number
    peso : number
    telefone : string
    --
}

entity Prontuario{
    *id : int <<generated>>
    ultimaConsulta : datetime
    proximaConsulta : datetime
    prescriptions : varchar(255)
    --
    *id_medico : int <<FK>>
    *id_paciente : ObjectId <<FK>>
}

entity UsuarioMedico{
    *id_medico : int <<generated>>
    nome : varchar(255)
    crm : varchar(255)
    especialidade : varchar(255)
    telefone : varchar(255)
    email : varchar(255)
    birthDate : date
    sexo : varchar(255)
    endereco : varchar(255)
    --
}

UsuarioMedico ||--o{ Prontuario
UsuarioPaciente ||--o{ Prontuario


@enduml