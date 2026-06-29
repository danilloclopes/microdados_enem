# Roteiro dos Microdados do ENEM — Dicionário de Variáveis (2020–2023)

Os dicionários de microdados do ENEM de **2020, 2021, 2022 e 2023 são completamente idênticos** em termos de variáveis, descrições, tipos e tamanhos. O arquivo de cada edição contém uma única aba principal com todos os campos do participante, seus resultados e as respostas ao questionário socioeconômico.

---

## Variáveis selecionadas no pipeline de análise

O notebook `enem_analise.ipynb` carrega apenas o subconjunto abaixo de cada arquivo Parquet. As demais variáveis existem nos microdados originais mas não são utilizadas.

```
NU_ANO
TP_FAIXA_ETARIA, TP_SEXO, TP_COR_RACA
TP_ST_CONCLUSAO, TP_ANO_CONCLUIU, IN_TREINEIRO
TP_ESCOLA, TP_DEPENDENCIA_ADM_ESC, TP_LOCALIZACAO_ESC
CO_MUNICIPIO_PROVA, NO_MUNICIPIO_PROVA, SG_UF_PROVA
TP_PRESENCA_CN, TP_PRESENCA_CH, TP_PRESENCA_LC, TP_PRESENCA_MT
NU_NOTA_CN, NU_NOTA_CH, NU_NOTA_LC, NU_NOTA_MT
NU_NOTA_COMP1, NU_NOTA_COMP2, NU_NOTA_COMP3, NU_NOTA_COMP4, NU_NOTA_COMP5
NU_NOTA_REDACAO, TP_STATUS_REDACAO
Q006
```

> **`NU_INSCRICAO` não é carregado.** Ele identifica um candidato individual e não representa um atributo analítico de perfil. A dimensão `DIM_CANDIDATO` é construída a partir de combinações únicas de atributos demográficos (sexo, raça/cor, faixa etária, segmento), o que reduz sua cardinalidade de ~16 milhões para algumas centenas de linhas.

---

## Roteiro completo das variáveis

O arquivo de microdados é organizado em grandes blocos temáticos. A seguir, cada variável é descrita em texto corrido, com seu nome técnico, tipo de dado, tamanho em caracteres e os valores possíveis quando se trata de campo categórico.

---

### Bloco 1 — Dados do Participante

O primeiro grupo de variáveis identifica e caracteriza o candidato inscrito.

**`NU_INSCRICAO`** é o número de inscrição do participante, campo numérico de 12 dígitos que funciona como identificador único de cada linha do arquivo. *Não é carregado no pipeline de análise — ver nota na seção acima.*

**`NU_ANO`** registra o ano de realização do ENEM, campo numérico de 4 dígitos.

**`TP_FAIXA_ETARIA`** indica a faixa etária do participante, campo numérico de 2 dígitos com 20 categorias: 1 = Menor de 17 anos, 2 = 17 anos, 3 = 18 anos, 4 = 19 anos, 5 = 20 anos, 6 = 21 anos, 7 = 22 anos, 8 = 23 anos, 9 = 24 anos, 10 = 25 anos, 11 = Entre 26 e 30 anos, 12 = Entre 31 e 35 anos, 13 = Entre 36 e 40 anos, 14 = Entre 41 e 45 anos, 15 = Entre 46 e 50 anos, 16 = Entre 51 e 55 anos, 17 = Entre 56 e 60 anos, 18 = Entre 61 e 65 anos, 19 = Entre 66 e 70 anos, 20 = Maior de 70 anos.

**`TP_SEXO`** indica o sexo do participante, campo alfanumérico de 1 caractere: M = Masculino, F = Feminino.

**`TP_ESTADO_CIVIL`** informa o estado civil, campo numérico de 1 dígito: 0 = Não informado, 1 = Solteiro(a), 2 = Casado(a)/Mora com companheiro(a), 3 = Divorciado(a)/Desquitado(a)/Separado(a), 4 = Viúvo(a).

**`TP_COR_RACA`** registra a cor ou raça autodeclarada, campo numérico de 1 dígito: 0 = Não declarado, 1 = Branca, 2 = Preta, 3 = Parda, 4 = Amarela, 5 = Indígena.

**`TP_NACIONALIDADE`** informa a nacionalidade do candidato, campo numérico de 1 dígito: 0 = Não informado, 1 = Brasileiro(a), 2 = Brasileiro(a) Naturalizado(a), 3 = Estrangeiro(a), 4 = Brasileiro(a) Nascido(a) no Exterior.

**`TP_ST_CONCLUSAO`** indica a situação de conclusão do Ensino Médio, campo numérico de 1 dígito: 1 = Já concluí o Ensino Médio, 2 = Estou cursando e concluirei no ano da prova, 3 = Estou cursando e concluirei após o ano da prova, 4 = Não concluí e não estou cursando o Ensino Médio.

**`TP_ANO_CONCLUIU`** registra o ano de conclusão do Ensino Médio para quem já concluiu, campo numérico de 1 dígito com categorias que variam de 0 = Não informado até valores que representam anos recentes (geralmente até 15 anos antes da edição do ENEM).

**`TP_ESCOLA`** indica o tipo de escola do Ensino Médio, campo numérico de 1 dígito: 1 = Não Respondeu, 2 = Pública, 3 = Privada, 4 = Exterior.

**`TP_ENSINO`** informa o tipo de instituição em que o candidato concluiu ou concluirá o Ensino Médio, campo numérico de 1 dígito: 1 = Ensino Regular, 2 = Educação Especial — Modalidade Substitutiva, 3 = Educação de Jovens e Adultos (EJA).

**`IN_TREINEIRO`** é um indicador binário que sinaliza se o inscrito realizou a prova apenas para treinar seus conhecimentos, sem utilizar o resultado para acesso ao ensino superior, campo numérico de 1 dígito: 1 = Sim, 0 = Não.

---

### Bloco 2 — Dados da Escola

Este bloco reúne informações sobre a escola onde o candidato cursou ou está cursando o Ensino Médio.

**`CO_MUNICIPIO_ESC`** é o código IBGE do município da escola, campo numérico de 7 dígitos.

**`NO_MUNICIPIO_ESC`** traz o nome do município da escola, campo alfanumérico de até 150 caracteres.

**`CO_UF_ESC`** é o código da Unidade da Federação da escola, campo numérico de 2 dígitos.

**`SG_UF_ESC`** traz a sigla da Unidade da Federação da escola, campo alfanumérico de 2 caracteres (ex.: SP, RJ, MG).

**`TP_DEPENDENCIA_ADM_ESC`** indica a dependência administrativa da escola, campo numérico de 1 dígito: 1 = Federal, 2 = Estadual, 3 = Municipal, 4 = Privada.

**`TP_LOCALIZACAO_ESC`** informa a localização da escola, campo numérico de 1 dígito: 1 = Urbana, 2 = Rural.

**`TP_SIT_FUNC_ESC`** registra a situação de funcionamento da escola, campo numérico de 1 dígito: 1 = Em atividade, 2 = Paralisada, 3 = Extinta, 4 = Escola inexistente na base do Censo Escolar.

---

### Bloco 3 — Dados do Local de Aplicação da Prova

Este bloco identifica onde o candidato realizou o exame.

**`CO_MUNICIPIO_PROVA`** é o código IBGE do município onde a prova foi aplicada, campo numérico de 7 dígitos.

**`NO_MUNICIPIO_PROVA`** traz o nome do município de aplicação da prova, campo alfanumérico de até 150 caracteres.

**`CO_UF_PROVA`** é o código da Unidade da Federação de aplicação da prova, campo alfanumérico de 2 dígitos.

**`SG_UF_PROVA`** é a sigla da Unidade da Federação de aplicação da prova, campo alfanumérico de 2 caracteres.

---

### Bloco 4 — Dados da Prova Objetiva

Este é o bloco central do desempenho acadêmico. Cobre as quatro áreas do conhecimento: Ciências da Natureza (CN), Ciências Humanas (CH), Linguagens e Códigos (LC) e Matemática (MT).

**`TP_PRESENCA_CN`**, **`TP_PRESENCA_CH`**, **`TP_PRESENCA_LC`** e **`TP_PRESENCA_MT`** registram, para cada área, se o candidato compareceu à prova. São campos numéricos de 1 dígito com os valores: 0 = Faltou à prova, 1 = Presente na prova, 2 = Eliminado na prova.

**`CO_PROVA_CN`**, **`CO_PROVA_CH`**, **`CO_PROVA_LC`** e **`CO_PROVA_MT`** trazem o código do tipo de prova aplicada em cada área (campo numérico de 3 dígitos). Cada edição do ENEM distribui diferentes versões da prova com cores (Azul, Amarela, Branca, Cinza, Rosa) e versões adaptadas para leitores com deficiência visual (Braille, Superampliada, Ampliada, Videoprova em Libras), além de versões em língua estrangeira para brasileiros que residem no exterior.

**`NU_NOTA_CN`**, **`NU_NOTA_CH`**, **`NU_NOTA_LC`** e **`NU_NOTA_MT`** são as notas obtidas em cada área, campos numéricos de 9 posições com casas decimais, calculadas pela Teoria de Resposta ao Item (TRI). O campo fica vazio quando o candidato foi ausente ou eliminado.

**`TX_RESPOSTAS_CN`**, **`TX_RESPOSTAS_CH`** e **`TX_RESPOSTAS_MT`** são vetores alfanuméricos de 45 caracteres que registram, letra a letra (A, B, C, D, E), as respostas marcadas pelo candidato nas 45 questões de cada caderno objetivo dessas três áreas. **`TX_RESPOSTAS_LC`** tem 45 caracteres também, mas inclui as questões de língua estrangeira (inglês ou espanhol) conforme a opção do candidato.

**`TP_LINGUA`** indica a língua estrangeira escolhida pelo participante para a prova de Linguagens e Códigos, campo numérico de 1 dígito: 0 = Inglês, 1 = Espanhol.

**`TX_GABARITO_CN`**, **`TX_GABARITO_CH`** e **`TX_GABARITO_MT`** são os gabaritos oficiais correspondentes aos cadernos de cada área, campos alfanuméricos de 45 caracteres. **`TX_GABARITO_LC`** tem 50 caracteres pois o caderno de Linguagens inclui tanto as questões comuns quanto as de língua estrangeira.

---

### Bloco 5 — Dados da Redação

Este bloco cobre a avaliação da prova dissertativo-argumentativa.

**`TP_STATUS_REDACAO`** indica a situação final da redação, campo numérico de 1 dígito: 1 = Sem problemas, 2 = Anulada, 3 = Cópia do Texto Motivador, 4 = Em Branco, 6 = Fuga ao tema, 7 = Não atendimento ao tipo textual, 8 = Texto insuficiente, 9 = Ilegível.

**`NU_NOTA_COMP1`** a **`NU_NOTA_COMP5`** são campos numéricos de 9 posições com a nota de cada uma das cinco competências avaliadas na redação, cada uma pontuada de 0 a 200 em intervalos de 40 pontos:

- **Competência 1** — Domínio da modalidade escrita formal da língua portuguesa.
- **Competência 2** — Compreensão da proposta e aplicação de conceitos das diversas áreas do conhecimento para desenvolver o tema dentro das regras do texto dissertativo-argumentativo em prosa.
- **Competência 3** — Capacidade de selecionar, relacionar, organizar e interpretar informações, fatos, opiniões e argumentos em defesa de um ponto de vista.
- **Competência 4** — Conhecimento dos mecanismos linguísticos necessários para a construção da argumentação.
- **Competência 5** — Elaboração de proposta de intervenção para o problema abordado, respeitando os direitos humanos.

**`NU_NOTA_REDACAO`** é a nota final da redação (soma das cinco competências), campo numérico de 9 posições, variando de 0 a 1000.

---

### Bloco 6 — Questionário Socioeconômico

O questionário socioeconômico é respondido no momento da inscrição e compõe 25 questões (Q001 a Q025), todas campos alfanuméricos de 1 caractere com respostas codificadas de A até G conforme a questão. Abaixo, cada questão é descrita com os valores possíveis.

**Q001** — Escolaridade do pai ou responsável masculino: A = Nunca estudou; B = Não completou o 5º ano do Ensino Fundamental; C = Completou o 5º ano, mas não o 9º ano do EF; D = Completou o EF, mas não o EM; E = Completou o EM, mas não a graduação; F = Completou a graduação ou mais; G = Não sei.

**Q002** — Escolaridade da mãe ou responsável feminina: mesmas categorias A a G da Q001.

**Q003** — Ocupação do pai ou responsável masculino: cinco grupos ordenados do Grupo 1 (trabalhadores rurais e domésticos) ao Grupo 5 (professores, militares de alta patente, profissionais liberais com pós-graduação, grandes empresários), além da categoria H = Nunca trabalhou.

**Q004** — Ocupação da mãe ou responsável feminina: mesmas categorias da Q003, com linguagem no feminino.

**Q005** — Número de pessoas que moram na residência, incluindo o candidato: 1 = mora sozinho, 2 = duas pessoas, até o valor máximo de 20 ou mais pessoas.

**Q006** — Renda mensal familiar total: A = Nenhuma renda; B = Até R$ 1.045,00; C = De R$ 1.045,01 até R$ 1.567,50; seguindo faixas crescentes até a categoria mais alta que representa rendas superiores a R$ 20.000,00. Os valores de corte variam ligeiramente entre edições para refletir correções monetárias.

**Q007** — Empregado(a) doméstico(a) na residência: A = Não; B = Sim, um ou dois dias por semana; C = Sim, três ou quatro dias por semana; D = Sim, cinco ou mais dias por semana (mensalista).

**Q008** — Número de banheiros na residência: A = Nenhum; B = Um; C = Dois; D = Três ou mais.

**Q009** — Número de quartos para dormir: A = Nenhum; B = Um; C = Dois; D = Três; E = Quatro ou mais.

**Q010** — Número de carros na residência: A = Nenhum; B = Um; C = Dois; D = Três ou mais.

**Q011** — Número de motocicletas: A = Nenhuma; B = Uma; C = Duas; D = Três ou mais.

**Q012** — Número de geladeiras: A = Nenhuma; B = Uma; C = Duas; D = Três ou mais.

**Q013** — Freezer (independente ou segunda porta da geladeira): A = Nenhum; B = Um; C = Dois; D = Três ou mais.

**Q014** — Máquina de lavar roupa (tanquinho não conta): A = Nenhuma; B = Uma; C = Duas; D = Três ou mais.

**Q015** — Máquina de secar roupa: A = Nenhuma; B = Uma; C = Duas; D = Três ou mais.

**Q016** — Forno micro-ondas: A = Nenhum; B = Um; C = Dois; D = Três ou mais.

**Q017** — Máquina de lavar louça: A = Nenhuma; B = Uma; C = Duas; D = Três ou mais.

**Q018** — Aspirador de pó: A = Não; B = Sim.

**Q019** — Televisão em cores: A = Nenhuma; B = Uma; C = Duas; D = Três ou mais.

**Q020** — Aparelho de DVD: A = Não; B = Sim.

**Q021** — TV por assinatura: A = Não; B = Sim.

**Q022** — Número de telefones celulares: A = Nenhum; B = Um; C = Dois; D = Três; E = Quatro ou mais.

**Q023** — Posse de telefone fixo na residência: A = Não; B = Sim.

**Q024** — Número de computadores na residência: A = Nenhum; B = Um; C = Dois; D = Três; E = Quatro ou mais.

**Q025** — Acesso à internet na residência: A = Não; B = Sim.

---

### Itens da Prova (aba separada: `ITENS_PROVA_AAAA`)

Todos os anos incluem uma aba adicional com o dicionário dos itens (questões) da prova objetiva. Essa aba é estável entre 2020 e 2023 e contém as seguintes variáveis:

**`CO_POSICAO`** — Posição do item na prova (campo numérico de 3 dígitos).

**`SG_AREA`** — Sigla da área de conhecimento do item: CH = Ciências Humanas, CN = Ciências da Natureza, LC = Linguagens e Códigos, MT = Matemática (campo alfanumérico de 2 caracteres).

As demais variáveis desta aba descrevem o código do item, o gabarito, os parâmetros TRI (discriminação, dificuldade e pseudo-chance), a posição na versão original e o indicador de item em língua estrangeira, entre outros metadados técnicos usados para a calibração e pontuação das provas.

---

### Questionário de Hábitos de Estudo durante a Pandemia (exclusivo de 2022)

Na edição de 2022, o dicionário inclui uma terceira aba chamada `QUEST_HAB_ESTUDO`, com 231 linhas descrevendo um questionário aplicado opcionalmente aos participantes sobre seus hábitos de estudo durante o período da pandemia de COVID-19. Essa aba não existe nas demais edições (2020, 2021 e 2023). As variáveis desta aba são identificadas por `NU_INSCRICAO` e `TP_RESPOSTA` (indicando se o participante optou por responder), seguidas de um conjunto extenso de perguntas temáticas sobre condições de estudo, acesso a recursos digitais e impacto da pandemia na preparação para o exame.

---

*Este roteiro foi gerado a partir da análise comparativa dos dicionários oficiais dos Microdados do ENEM publicados pelo INEP para as edições de 2020, 2021, 2022 e 2023.*
