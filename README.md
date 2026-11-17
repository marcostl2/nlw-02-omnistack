# Proffy

Procure um professor pela matéria, pelo dia da semana e pelo horário em que você pode estudar. Cada resultado reúne apresentação, preço por hora e contato por WhatsApp.

Projeto da Next Level Week 2, da Rocketseat, com cadastro de professores na web e busca de aulas na web e no celular.

![Apresentação do Proffy](.github/proffy.png)

## Para quem ensina

O formulário web cadastra os dados do professor, a matéria, o valor da hora e os períodos disponíveis. É possível informar mais de um horário.

No servidor, o cadastro salva professor, aula e disponibilidade em uma transação. Os horários são convertidos em minutos para a consulta de disponibilidade.

## Para quem estuda

A busca exige matéria, dia da semana e horário. Os resultados mostram foto, nome, bio e preço por hora, com um botão para entrar em contato.

No aplicativo, professores também podem ser salvos como favoritos. Essa lista fica no aparelho, usando AsyncStorage. A tela mobile para quem deseja ensinar orienta a fazer o cadastro pela web.

Quando alguém aciona o contato, o cliente envia um registro para a API. O total de conexões exibido na página inicial corresponde a esses registros.

## Estrutura do projeto

| Pasta | Conteúdo |
| --- | --- |
| `web/` | Interface em React 16 e TypeScript, com React Router e CSS |
| `mobile/` | Aplicativo em React Native e TypeScript, com Expo SDK 38 e React Navigation |
| `server/` | API em Node.js e TypeScript, com Express, Knex e SQLite |
| `.github/` | Logo e imagem de apresentação |

O banco relaciona `users`, `classes`, `class_schedule` e `connections`. As definições estão nas [migrations](server/src/database/migrations).

## Endpoints

| Método | Rota | O que faz |
| --- | --- | --- |
| POST | `/classes` | Cadastra professor, aula e horários disponíveis |
| GET | `/classes` | Consulta aulas por matéria, dia e horário |
| POST | `/connections` | Registra uma tentativa de contato com um professor |
| GET | `/connections` | Retorna o total de conexões registradas |

Para consultar aulas, envie os três parâmetros: `subject`, `week_day` e `time`. O horário deve seguir o formato `HH:MM`. Sem os três filtros, a API responde com status `400`.

## Ambiente de desenvolvimento

Instale as dependências de `server/`, `web/` e `mobile/` separadamente. Cada aplicação é iniciada em seu próprio terminal.

No servidor, os comandos definidos são:

```sh
npm run knex:migrate
npm start
```

O primeiro aplica as migrations no SQLite configurado em [server/knexfile.ts](server/knexfile.ts). O segundo inicia a API na porta `3333`.

Na web e no mobile, o comando de desenvolvimento é `npm start`. A web aponta para `http://localhost:3333`. Para usar o aplicativo em um aparelho, ajuste o endereço em [mobile/src/services/api.ts](mobile/src/services/api.ts) para uma máquina acessível pela rede.

As versões de React, Expo e demais bibliotecas são as registradas no projeto do curso. Os comandos acima foram lidos no código; esta revisão do README não incluiu instalação, atualização de dependências ou execução.

## Layouts e créditos

Os arquivos de referência do curso estão no Figma:

- [Layout web](https://www.figma.com/file/GHGS126t7WYjnPZdRKChJF/Proffy-Web)
- [Layout mobile](https://www.figma.com/file/e33KvgUpFdunXxJjHnK7CG/Proffy-Mobile)

A imagem de apresentação usada neste README já faz parte do repositório.

Projeto e materiais originais da Rocketseat. Licença [MIT](LICENSE.md).
