# Domínios do RESUMIUM

## Visão geral

O RESUMIUM recebe informações profissionais do usuário e as transforma em um currículo sob medida, otimizado com inteligência artificial para a descrição da vaga fornecida.

## Resume

O objeto `Resume` representa o perfil profissional permanente. A descrição da vaga deve ser fornecida separadamente em cada solicitação de geração e pertencer ao futuro fluxo do domínio `Application`, não ao perfil.

Datas usam o formato `YYYY-MM-DD`; valores opcionais sem informação usam `null`, e coleções sem itens usam arrays vazios. A geração deve reorganizar fatos do perfil sem inventar qualificações ou resultados.

### Exemplo de `resume.json`

```json
{
  "name": "Alex",
  "lastName": "Example",
  "headline": "Software Engineer",
  "email": "alex@example.com",
  "phoneNumber": null,
  "location": "São Paulo, SP, Brasil",
  "githubUrl": "https://github.com/alex-example",
  "linkedinUrl": "https://www.linkedin.com/in/alex-example",
  "portfolioUrl": null,
  "summary": "Resumo profissional fictício para demonstrar o formato do campo.",
  "workExperiences": [
    {
      "companyName": "Example Tecnologia",
      "jobTitle": "Software Engineer",
      "description": "Descrição fictícia das responsabilidades da função.",
      "achievements": [
        "Exemplo fictício de resultado mensurável, sujeito a validação pela pessoa."
      ],
      "isCurrent": true,
      "startDate": "2023-05-12",
      "endDate": null
    }
  ],
  "education": [
    {
      "degree": "Bachelor's Degree",
      "courseName": "Computer Engineering",
      "institutionName": "Example University",
      "location": "São Paulo, SP, Brasil",
      "isInProgress": false,
      "startDate": "2018-02-20",
      "endDate": "2022-12-15"
    }
  ],
  "projects": [
    {
      "projectName": "Example URL Shortener",
      "description": "Projeto fictício para demonstrar a estrutura.",
      "technologies": ["TypeScript", "PostgreSQL"],
      "url": "https://github.com/alex-example/url-shortener"
    }
  ],
  "courses": [
    {
      "courseName": "Advanced JavaScript",
      "institutionName": "Example Learning Platform",
      "isCompleted": true,
      "startDate": "2024-05-12",
      "endDate": "2024-06-23"
    }
  ],
  "certifications": [
    {
      "certificationName": "Example Cloud Certification",
      "issuerName": "Example Cloud Provider",
      "credentialId": null,
      "credentialUrl": null,
      "issueDate": "2025-03-10",
      "expirationDate": null
    }
  ],
  "hardSkills": [
    {
      "name": "TypeScript",
      "level": "advanced"
    }
  ],
  "softSkills": [
    {
      "name": "Problem solving"
    }
  ],
  "languages": [
    {
      "name": "Portuguese",
      "level": "native"
    },
    {
      "name": "English",
      "level": "advanced"
    }
  ]
}
```

### Proposta de validação

O contrato abaixo usa JSON Schema Draft 2020-12. Ele mantém uma estrutura estável: todas as propriedades previstas devem existir, mesmo quando o dado ainda não foi informado. A ausência de um valor escalar opcional é representada por `null`; uma coleção sem itens é representada por `[]`. Strings vazias ou formadas apenas por espaços não são aceitas.

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "title": "Resume",
  "type": "object",
  "additionalProperties": false,
  "required": [
    "name",
    "lastName",
    "headline",
    "email",
    "phoneNumber",
    "location",
    "githubUrl",
    "linkedinUrl",
    "portfolioUrl",
    "summary",
    "workExperiences",
    "education",
    "projects",
    "courses",
    "certifications",
    "hardSkills",
    "softSkills",
    "languages"
  ],
  "properties": {
    "name": { "$ref": "#/$defs/nonEmptyString" },
    "lastName": { "$ref": "#/$defs/nonEmptyString" },
    "headline": { "$ref": "#/$defs/nonEmptyString" },
    "email": {
      "type": "string",
      "format": "email",
      "minLength": 1,
      "pattern": "\\S"
    },
    "phoneNumber": { "$ref": "#/$defs/nullableNonEmptyString" },
    "location": { "$ref": "#/$defs/nonEmptyString" },
    "githubUrl": { "$ref": "#/$defs/nullableHttpUrl" },
    "linkedinUrl": { "$ref": "#/$defs/nullableHttpUrl" },
    "portfolioUrl": { "$ref": "#/$defs/nullableHttpUrl" },
    "summary": { "$ref": "#/$defs/nonEmptyString" },
    "workExperiences": {
      "type": "array",
      "items": { "$ref": "#/$defs/workExperience" }
    },
    "education": {
      "type": "array",
      "items": { "$ref": "#/$defs/education" }
    },
    "projects": {
      "type": "array",
      "items": { "$ref": "#/$defs/project" }
    },
    "courses": {
      "type": "array",
      "items": { "$ref": "#/$defs/course" }
    },
    "certifications": {
      "type": "array",
      "items": { "$ref": "#/$defs/certification" }
    },
    "hardSkills": {
      "type": "array",
      "items": { "$ref": "#/$defs/hardSkill" }
    },
    "softSkills": {
      "type": "array",
      "items": { "$ref": "#/$defs/softSkill" }
    },
    "languages": {
      "type": "array",
      "items": { "$ref": "#/$defs/language" }
    }
  },
  "$defs": {
    "nonEmptyString": {
      "type": "string",
      "minLength": 1,
      "pattern": "\\S"
    },
    "nullableNonEmptyString": {
      "anyOf": [
        { "$ref": "#/$defs/nonEmptyString" },
        { "type": "null" }
      ]
    },
    "httpUrl": {
      "type": "string",
      "format": "uri",
      "minLength": 1,
      "pattern": "^[Hh][Tt][Tt][Pp][Ss]?://\\S+$"
    },
    "nullableHttpUrl": {
      "anyOf": [
        { "$ref": "#/$defs/httpUrl" },
        { "type": "null" }
      ]
    },
    "date": {
      "type": "string",
      "format": "date"
    },
    "nullableDate": {
      "anyOf": [
        { "$ref": "#/$defs/date" },
        { "type": "null" }
      ]
    },
    "workExperience": {
      "type": "object",
      "additionalProperties": false,
      "required": [
        "companyName",
        "jobTitle",
        "description",
        "achievements",
        "isCurrent",
        "startDate",
        "endDate"
      ],
      "properties": {
        "companyName": { "$ref": "#/$defs/nonEmptyString" },
        "jobTitle": { "$ref": "#/$defs/nonEmptyString" },
        "description": { "$ref": "#/$defs/nonEmptyString" },
        "achievements": {
          "type": "array",
          "uniqueItems": true,
          "items": { "$ref": "#/$defs/nonEmptyString" }
        },
        "isCurrent": { "type": "boolean" },
        "startDate": { "$ref": "#/$defs/date" },
        "endDate": { "$ref": "#/$defs/nullableDate" }
      },
      "allOf": [
        {
          "if": {
            "properties": { "isCurrent": { "const": true } },
            "required": ["isCurrent"]
          },
          "then": {
            "properties": { "endDate": { "type": "null" } }
          },
          "else": {
            "properties": { "endDate": { "$ref": "#/$defs/date" } }
          }
        }
      ]
    },
    "education": {
      "type": "object",
      "additionalProperties": false,
      "required": [
        "degree",
        "courseName",
        "institutionName",
        "location",
        "isInProgress",
        "startDate",
        "endDate"
      ],
      "properties": {
        "degree": { "$ref": "#/$defs/nonEmptyString" },
        "courseName": { "$ref": "#/$defs/nonEmptyString" },
        "institutionName": { "$ref": "#/$defs/nonEmptyString" },
        "location": { "$ref": "#/$defs/nullableNonEmptyString" },
        "isInProgress": { "type": "boolean" },
        "startDate": { "$ref": "#/$defs/date" },
        "endDate": { "$ref": "#/$defs/nullableDate" }
      },
      "allOf": [
        {
          "if": {
            "properties": { "isInProgress": { "const": true } },
            "required": ["isInProgress"]
          },
          "then": {
            "properties": { "endDate": { "type": "null" } }
          },
          "else": {
            "properties": { "endDate": { "$ref": "#/$defs/date" } }
          }
        }
      ]
    },
    "project": {
      "type": "object",
      "additionalProperties": false,
      "required": [
        "projectName",
        "description",
        "technologies",
        "url"
      ],
      "properties": {
        "projectName": { "$ref": "#/$defs/nonEmptyString" },
        "description": { "$ref": "#/$defs/nonEmptyString" },
        "technologies": {
          "type": "array",
          "uniqueItems": true,
          "items": { "$ref": "#/$defs/nonEmptyString" }
        },
        "url": { "$ref": "#/$defs/nullableHttpUrl" }
      }
    },
    "course": {
      "type": "object",
      "additionalProperties": false,
      "required": [
        "courseName",
        "institutionName",
        "isCompleted",
        "startDate",
        "endDate"
      ],
      "properties": {
        "courseName": { "$ref": "#/$defs/nonEmptyString" },
        "institutionName": { "$ref": "#/$defs/nonEmptyString" },
        "isCompleted": { "type": "boolean" },
        "startDate": { "$ref": "#/$defs/nullableDate" },
        "endDate": { "$ref": "#/$defs/nullableDate" }
      },
      "allOf": [
        {
          "if": {
            "properties": { "isCompleted": { "const": false } },
            "required": ["isCompleted"]
          },
          "then": {
            "properties": { "endDate": { "type": "null" } }
          },
          "else": {
            "properties": { "endDate": { "$ref": "#/$defs/date" } }
          }
        }
      ]
    },
    "certification": {
      "type": "object",
      "additionalProperties": false,
      "required": [
        "certificationName",
        "issuerName",
        "credentialId",
        "credentialUrl",
        "issueDate",
        "expirationDate"
      ],
      "properties": {
        "certificationName": { "$ref": "#/$defs/nonEmptyString" },
        "issuerName": { "$ref": "#/$defs/nonEmptyString" },
        "credentialId": { "$ref": "#/$defs/nullableNonEmptyString" },
        "credentialUrl": { "$ref": "#/$defs/nullableHttpUrl" },
        "issueDate": { "$ref": "#/$defs/date" },
        "expirationDate": { "$ref": "#/$defs/nullableDate" }
      }
    },
    "hardSkill": {
      "type": "object",
      "additionalProperties": false,
      "required": ["name", "level"],
      "properties": {
        "name": { "$ref": "#/$defs/nonEmptyString" },
        "level": {
          "type": "string",
          "enum": ["basic", "intermediate", "advanced"]
        }
      }
    },
    "softSkill": {
      "type": "object",
      "additionalProperties": false,
      "required": ["name"],
      "properties": {
        "name": { "$ref": "#/$defs/nonEmptyString" }
      }
    },
    "language": {
      "type": "object",
      "additionalProperties": false,
      "required": ["name", "level"],
      "properties": {
        "name": { "$ref": "#/$defs/nonEmptyString" },
        "level": {
          "type": "string",
          "enum": ["basic", "intermediate", "advanced", "native"]
        }
      }
    }
  }
}
```

### Obrigatoriedade e ausência de informação

| Grupo | Obrigatórios e não anuláveis | Aceitam `null` | Aceitam `[]` |
| --- | --- | --- | --- |
| Perfil | `name`, `lastName`, `headline`, `email`, `location`, `summary` | `phoneNumber`, `githubUrl`, `linkedinUrl`, `portfolioUrl` | Todas as coleções do perfil |
| Experiência | `companyName`, `jobTitle`, `description`, `isCurrent`, `startDate` | `endDate` somente quando `isCurrent` for `true` | `achievements` |
| Formação | `degree`, `courseName`, `institutionName`, `isInProgress`, `startDate` | `location`; `endDate` somente quando `isInProgress` for `true` | — |
| Projeto | `projectName`, `description` | `url` | `technologies` |
| Curso | `courseName`, `institutionName`, `isCompleted` | `startDate`; `endDate` somente quando `isCompleted` for `false` | — |
| Certificação | `certificationName`, `issuerName`, `issueDate` | `credentialId`, `credentialUrl`, `expirationDate` | — |
| Hard skill | `name`, `level` | — | A coleção `hardSkills` |
| Soft skill | `name` | — | A coleção `softSkills` |
| Idioma | `name`, `level` | — | A coleção `languages` |

Todas as propriedades da tabela são obrigatórias na estrutura. A coluna “Aceitam `null`” identifica os dados opcionais para o usuário. Um campo obrigatório sem informação torna o objeto inválido; ele não deve ser enviado como `null`, `""` ou omitido. Da mesma forma, itens vazios dentro de `achievements` e `technologies` são inválidos.

### Valores controlados

- `hardSkills[].level`: `basic`, `intermediate` ou `advanced`.
- `languages[].level`: `basic`, `intermediate`, `advanced` ou `native`.
- Campos booleanos aceitam somente `true` ou `false`.
- Datas aceitam o formato `YYYY-MM-DD`.
- URLs aceitam somente os protocolos HTTP e HTTPS.

Os níveis são separados porque `native` descreve proficiência em um idioma, mas não uma habilidade técnica. Os três níveis de hard skill mantêm a resposta simples e comparável para a futura seleção de competências pela aplicação.

### Decisões de modelagem

A estrutura estável evita que propriedade ausente, string vazia e `null` representem o mesmo estado. Isso simplifica formulários, persistência, inferência de tipos e a preparação dos dados enviados à inteligência artificial. `null` significa que um valor escalar opcional ainda não foi informado; `[]` significa que a coleção foi informada, mas não contém itens.

O telefone não possui uma expressão regular específica porque números nacionais e internacionais podem ter formatos de exibição diferentes. Quando presente, ainda precisa ser uma string com algum caractere que não seja espaço. E-mail, URLs e datas possuem validações de formato porque seguem padrões bem definidos.

As condições entre o estado de um item e `endDate` evitam combinações contraditórias, como uma experiência atual com data de término. A comparação cronológica entre datas, por exemplo `endDate >= startDate`, deve ser adicionada na futura implementação com Zod, pois essa regra não é expressa de forma portátil pelo JSON Schema.

### Implementação futura com Zod

Na implementação, Zod 4 deve se tornar a fonte do contrato. Os objetos devem ser estritos; os enums devem usar `z.enum`; e-mail, URLs e datas devem usar `z.email()`, `z.httpUrl()` e `z.iso.date()`. Campos escalares opcionais no domínio devem usar `.nullable()`, sem `.optional()`, preservando a exigência de que a propriedade exista. Regras entre propriedades e comparações cronológicas devem usar `.superRefine()`.

O tipo TypeScript deverá ser inferido do schema com `z.infer`. O JSON Schema poderá então ser gerado com `z.toJSONSchema()`, evitando divergência entre documentação, validação em runtime e tipos da aplicação.
