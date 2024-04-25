# 1 - Changelog
|#| Descrição | Épico | Feature | UserStory | Issue/Bug |
|--|--|--|--|--|--|
| 1 | Design de novo layout de tela | #1166 | #2021 | #2022 |  |

# 2 - Definição
O Ponto de Equipamento tem como finalidade registrar o trabalho realizado pelo equipamento na obra quando o seu contrato é definido como pagamento diário, mensal, ou por hora, independente do trabalho realizado.
Quando o equipamento possui um desses três tipos de contrato o seu ponto deve ser lançado na obra diariamente, bem como suas faltas e seus respectivos motivos.

Por padrão um equipamento deve ter seu ponto lançado em todos os dias em que possui contrato na obra. Entretanto caso no contrato esteja sinalizado que não é necessário exigir o lançamento de ponto todos os dias, o lançamento passa a ser opcional.

Existem duas situações para o lançamento de um Ponto de Equipamento que definem as características de cada lançamento: Quando o equipamento PRODUZIU, e quando o equipamento NÃO PRODUZIU.

A seguir detalhamos as características de cada forma de lançamento.

# 3 - Dados Gerais
Para que um Ponto de Equipamento seja lançado existem dados que precisam ser informados que são gerais do ponto, independentemente se houve ou não produção no dia. São eles:

- **Equipamento**: Equipamento no qual o ponto está sendo registrado;
- **Operador**: Colaborador da Caiapó que opera o equipamento em obra;
- **Data**: Dia de trabalho do equipamento;
- **Controlado por**: Indica se o equipamento é controlado por Hora, KM, ou nenhuma das duas opções;
- **Horimetro ou Odometro inicial**: Valor que estava registrado no equipamento quando começou o dia de trabalho;
- **Horimetro ou Odometro final**: Valor que estava registrado no equipamento no momento que finalizou o dia de trabalho;
- **Quantidade de Horas/Km**: Quantidade de horas/km trabalhadas/rodados no dia.

Os detalhes dessas informações serão apresentadas nas regras de formulário.

# 4 - Quando Há Produção
Dizer que um equipamento produziu no dia significa que ele executou qualquer tipo de atividade na obra para atender a um determinado serviço. Ele pode ter realizado algum transporte de material, feito roçagem, pavimentação, compactação,  e assim por diante.

Quando um equipamento produziu o seu Ponto de Equipamento é feito de forma bem simplificada informando os seguintes dados:

- **Serviço**: O serviço a qual o equipamento estava atendendo quando estava trabalhando no dia;
- **Horas Mecânicas**: Horário, e quantidade de horas, que o equipamento ficou parado para manutenção, mesmo tendo produzido em alguma parte do dia.

Os detalhes dessas informações serão apresentadas nas regras de formulário.

# 5 - Quando Não Há Produção
Quando o equipamento não realiza nenhum tipo de atividade na obra, independentemente do motivo, dizemos que o equipamento "Não Produziu".
Nesta situação, ao realizar o lançamento de um Ponto de Equipamento, é necessário informar o Motivo pelo qual não houve produção do equipamento no dia. Os motivos são os seguintes:

- **A disposição da Obra**: Significa que o equipamento não produziu por alguma situação de competência da obra;
- **A disposição do Proprietário**: Significa que o equipamento não produziu por não estar disponível para a Obra devido à alguma necessidade do fornecedor do equipamento;
- **Folga de Pagamento**: Significa que o equipamento não produziu por paralização na obra, que pode ser por causa de um feriado, recesso, ou algum outro motivo forma de não atividade na obra.
- **Horas Mecânicas**: Significa que o equipamento não produziu no dia por ter ficado todo o dia em manutenção.

Os detalhes dessas informações serão apresentadas nas regras de formulário.

# 6 - Dados do Formulário

|Campo (Label)|Tipo|Obrigatório|Valor Automático|Regras|
|--|--|--|--|--|
|Equipamento|select|Sim|Não|[RN-01](#rn-01)|
|Operador|select|Sim|Não|[RN-02](#rn-02)|
|Número|inteiro|Sim|Sim|[RN-03](#rn-03)|
|Data|date|Sim|Sim *|[RN-04](#rn-04)|
|Controlado por|radio|Sim|Sim *|[RN-05](#rn-05)|
|Odômetro Inicial|inteiro|Sim **|Sim *|[RN-06](#rn-06)|
|Odômetro Final|inteiro|Sim **|Não|[RN-07](#rn-07)|
|Horímetro Inicial|decimal|Sim **|Sim *|[RN-08](#rn-08)|
|Horímetro Final|decimal|Sim **|Não|[RN-09](#rn-09)|
|Quant. KM|inteiro|Sim|Sim|[RN-10](#rn-10)|
|Quant. Horas|decimal|Sim|Sim|[RN-11](#rn-11)|
|Valor Unitário|decimal|Sim|Sim *|[RN-12](#rn-12)|
|Valor Bruto|decimal|Sim|Sim *|[RN-13](#rn-13)|
|Valor Desconto|decimal|Sim|Sim *|[RN-14](#rn-14)|
|Valor a Pagar|decimal|Sim|Sim *|[RN-15](#rn-15)|
|Observação|text|Sim **|Não|[RN-16](#rn-16)|

## 6.1 - Quando há produção
|Campo (Label)|Tipo|Obrigatório|Valor Automático|Regras|
|--|--|--|--|--|
|Serviços|multi select|Sim|Não|[RN-17](#rn-17)|
|Horas Mecânicas|lista|Não|Não|[RN-18](#rn-18)|
|Total de Horas|time|Não **|Sim|[RN-19](#rn-19)|

## 6.2 - Quando não há produção
|Campo (Label)|Tipo|Obrigatório|Valor Automático|Regras|
|--|--|--|--|--|
|Motivo da Não Produção|radio|Sim|Não|[RN-20](#rn-20)|

( * ) O preenchimento automático do campo é condicional;
( ** ) A obrigatoriedade é condicional.

# 7 - Regras de Negócio
## 7.1 - Regras de Formulário
- **<span id="rn-01">RN-01</span>**: O campo **_Equipamento_** é obrigatório e de seleção única;
   - **<span id="rn-01-01">RN-01-01</span>**: Quando o usuário possui permissão para lançar ponto com pendência de equipamento sem contrato, devem ser listados todos os equipamentos ativos;
   - **<span id="rn-01-02">RN-01-02</span>**: Quando o usuário NÃO possui permissão para lançar ponto com pendência de equipamento sem contrato, devem ser listados os equipamentos ativos que possuem algum tipo de contrato na obra;
   - **<span id="rn-01-03">RN-01-03</span>**: Quando o usuário possui permissão para lançar ponto com pendência de equipamento não cadastrado, deve ser possível ele digitar somente a placa do equipamento caso o mesmo não esteja listado para ser selecionado;
   - **<span id="rn-01-04">RN-01-04</span>**: Quando o usuário NÃO possui permissão para lançar ponto com pendência de equipamento não cadastrado, o usuário obrigatoriamente deve selecionar um dos equipamentos listados.

- **<span id="rn-02">RN-02</span>**: O campo do _**Operador**_ é obrigatório e de seleção única;
   - **<span id="rn-02-01">RN-02-01</span>**: Lista todos os operadores que estão ligados ao equipamento no cadastro de Setor Equipe da obra;

- **<span id="rn-03">RN-03</span>**: O campo **_Número_** é gerado automaticamente pelo banco de dados, em auto incremento;
   - **<span id="rn-03-01">RN-03-01</span>**: Por ser um campo de preenchimento automático ele deve estar sempre bloqueado e com a coloração cinza, diferenciando dos demais campos editáveis;
   - **<span id="rn-03-02">RN-03-02</span>**: Em nenhuma circunstância este campo deve ficar habilitado para edição.

- **<span id="rn-04">RN-04</span>**: O campo **_Data_** é de preenchimento obrigatório e não pode ser uma data futura;
   - **<span id="rn-04-01">RN-04-01</span>**: Se ainda não há nenhum Ponto de Equipamento lançado no sistema, em qualquer obra, o campo deve ficar habilitado para que seu valor seja informado manualmente;
   - **<span id="rn-04-02">RN-04-02</span>**: Se ainda não há nenhum Ponto de Equipamento lançado na obra, mas já houve lançamento em outras obras, o campo deve ficar desabilitado para edição e vir preenchido com a data subsequente ao último ponto lançado para o equipamento, seja qual for a obra em que foi lançado;
   - **<span id="rn-04-03">RN-04-03</span>**: Se há Ponto de Equipamento lançado na obra o campo deve ficar desabilitado para edição e vir preenchido com a data subsequente ao último ponto lançado para o equipamento na obra.
   - **<span id="rn-04-04">RN-04-04</span>**: Se o usuário tiver permissão para alterar a data do ponto deve ser possível que o campo seja habilitado para informação manual;
   - **<span id="rn-04-05">RN-04-05</span>**: Enquanto o campo estiver desabilitado para edição ele deve ficar na coloração cinza diferenciando dos demais campos editáveis.

- **<span id="rn-05">RN-05</span>**: O campo **_Controlado por_**, apesar de ser de exibição obrigatória no formulário ele não é um campo persistido. Ele é apenas uma representação;
   - **<span id="rn-05-01">RN-05-01</span>**: Quando lançar um novo ponto:
      - Se na categoria do equipamento está sinalizado que o Horimetro é obrigatório, então o campo vem preenchido com o valor "Hora";
      - Se na categoria do equipamento está sinalizado que o Odômetro é obrigatório, então o campo vem preenchido com o valor "Km";
      - Caso contrário o campo vem preenchido com o valor "Nenhum".
   - **<span id="rn-05-02">RN-05-02</span>**: Quando exibir um ponto já lançado, seja para edição ou somente para visualização:
      - Se foi informado o campo "Horímetro", então o campo vem preenchido com o valor "Hora";
      - Se foi informado o campo "Odômetro", então o campo vem preenchido com o valor "Km";
      - Caso contrário o campo vem preenchido com o valor "Nenhum".

- **<span id="rn-06">RN-06</span>**: O campo **_Odômetro Inicial_** é de preenchimento obrigatório somente se o equipamento for controlado por "Km";
   - **<span id="rn-06-01">RN-06-01</span>**: O campo deve estar visível no formulário somente se o equipamento for controlado por "Km";
   - **<span id="rn-06-02">RN-06-02</span>**: Se ainda não há nenhum ponto lançado para o equipamento em qualquer obra, o campo deve ficar habilitado para que seu valor seja informado manualmente;
   - **<span id="rn-06-03">RN-06-03</span>**: Se ainda não há nenhum Ponto de Equipamento lançado na obra, mas já houve lançamento em outras obras, o campo deve ficar desabilitado vir preenchido com o valor do "Odômetro Final" do último lançamento, seja qual for a obra em que foi lançado;
   - **<span id="rn-06-04">RN-06-04</span>**: Se há Ponto de Equipamento lançado na obra o campo deve ficar desabilitado e vir preenchido com o valor do campo "Odômetro Final" do último ponto de equipamento na obra;
   - **<span id="rn-06-05">RN-06-05</span>**: Se o usuário tiver permissão para alterar odômetro, deve ser possível habilitar o campo para que seu valor seja informado manualmente;
   - **<span id="rn-06-05">RN-06-06</span>**: Em casos de o valor ser informado manualmente via permissão, o mesmo deve ser maior ou igual ao "Odômetro Final" do último lançamento.
   - **<span id="rn-06-06">RN-06-06</span>**: Enquanto o campo estiver desabilitado para edição ele deve ficar na coloração cinza diferenciando dos demais campos editáveis.

- **<span id="rn-07">RN-07</span>**: O campo **_Odômetro Final_** é de preenchimento obrigatório somente se o equipamento for controlado por "Km";
   - **<span id="rn-07-01">RN-07-01</span>**: O campo deve estar visível no formulário somente se o equipamento for controlado por "Km";
   - **<span id="rn-07-02">RN-07-02</span>**: O valor informado deve ser maior que o campo "Odômetro Inicial";
   - **<span id="rn-07-03">RN-07-03</span>**: Para os casos de Não Produção o valor do campo deve ser exatamente igual ao  "Odômetro Inicial";

- **<span id="rn-08">RN-08</span>**: O campo **_Horíometro Inicial_** é de preenchimento obrigatório somente se o equipamento for controlado por "Km";
   - **<span id="rn-08-01">RN-08-01</span>**: O campo deve estar visível no formulário somente se o equipamento for controlado por "Hora";
   - **<span id="rn-08-02">RN-08-02</span>**: Se ainda não há nenhum ponto lançado para o equipamento em qualquer obra, o campo deve ficar habilitado para que seu valor seja informado manualmente;
   - **<span id="rn-08-03">RN-08-03</span>**: Se ainda não há nenhum Ponto de Equipamento lançado na obra, mas já houve lançamento em outras obras, o campo deve ficar desabilitado vir preenchido com o valor do "Horimetro Final" do último lançamento, seja qual for a obra em que foi lançado;
   - **<span id="rn-08-04">RN-08-04</span>**: Se há Ponto de Equipamento lançado na obra o campo deve ficar desabilitado e vir preenchido com o valor do campo "Horimetro Final" do último ponto de equipamento na obra;
   - **<span id="rn-08-05">RN-08-05</span>**: Se o usuário tiver permissão para alterar horimetro, deve ser possível habilitar o campo para que seu valor seja informado manualmente;
   - **<span id="rn-08-06">RN-08-06</span>**: Em casos de o valor ser informado manualmente via permissão, o mesmo deve ser maior ou igual ao "Horimetro Final" do último lançamento.
   - **<span id="rn-08-07">RN-08-07</span>**: Enquanto o campo estiver desabilitado para edição ele deve ficar na coloração cinza diferenciando dos demais campos editáveis.
   - **<span id="rn-08-08">RN-08-08</span>**: O campo deve ser formatado com 1 casa decimal. Ex.: (1324,7)

- **<span id="rn-09">RN-09</span>**: O campo **_Horíometro Final_** é de preenchimento obrigatório somente se o equipamento for controlado por "Km";
   - **<span id="rn-09-01">RN-09-01</span>**: O campo deve estar visível no formulário somente se o equipamento for controlado por "Hora";
   - **<span id="rn-09-02">RN-09-02</span>**: O valor informado deve ser maior que o campo "Horimetro Inicial";
   - **<span id="rn-09-03">RN-09-03</span>**: Para os casos de Não Produção o valor do campo deve ser exatamente igual ao  "Horimetro Inicial";
   - **<span id="rn-09-04">RN-09-04</span>**: O campo deve ser formatado com 1 casa decimal. Ex.: (1324,7)

- **<span id="rn-10">RN-10</span>**: O campo **_Quant. KM** é obrigatório somente se o equipamento for controlado por "Km";
   - **<span id="rn-10-01">RN-10-01</span>**: O campo deve estar visível no formulário somente se o equipamento for controlado por "Km";
   - **<span id="rn-10-02">RN-10-02</span>**: O campo é calculado automaticamente, devendo ficar sempre desabilitado e com a coloração cinza, de forma a diferenciar dos demais campos editáveis;
   - **<span id="rn-10-03">RN-10-03</span>**: O valor do campo se dá pela seguinte formula (OdometroFinal- OdometroInicial);

- **<span id="rn-11">RN-11</span>**: O campo **_Quant. Horas** é obrigatório somente se o equipamento for controlado por "Hora";
   - **<span id="rn-11-01">RN-11-01</span>**: O campo deve estar visível no formulário somente se o equipamento for controlado por "Hora";
   - **<span id="rn-11-02">RN-11-02</span>**: O campo é calculado automaticamente, devendo ficar sempre desabilitado e com a coloração cinza, de forma a diferenciar dos demais campos editáveis;
   - **<span id="rn-11-03">RN-11-03</span>**: O valor do campo se dá pela seguinte formula (HorimetroFinal- HorimetroInicial);
   - **<span id="rn-11-04">RN-11-04</span>**: O campo deve ser formatado com 1 casa decimal. Ex.: (1324,7)

- **<span id="rn-12">RN-12</span>**: O campo **_Valor Unitário_** é obrigatório e de preenchimento automático de acordo com o contrato do equipamento;
   - **<span id="rn-12-01">RN-12-01</span>**: Se o equipamento não possui contrato de ponto na obra o campo deve vir zerado (R$ 0,00);
   - **<span id="rn-12-02">RN-12-02</span>**: Se o equipamento possui contrato por Hora o campo deve vir preenchido com o valor do contrato que representa o valor a ser pago por hora trabalhada;
   - **<span id="rn-12-03">RN-12-03</span>**: Se o equipamento possui contrato por Dia o campo deve vir preenchido com o valor do contrato que representa o valor a ser pago por dia trabalhado;
   - **<span id="rn-12-04">RN-12-04</span>**: Se o equipamento possui contrato por Mês o campo deve vir preenchido com o valor do contrato que representa o valor a ser pago pelo mês trabalhado;
   - **<span id="rn-12-05">RN-12-05</span>**: Por ser um campo de preenchimento automático o mesmo deve estar sempre desabilitado e com a coloração cinza, de forma a diferenciar dos demais campos editáveis;
   - **<span id="rn-12-06">RN-12-06</span>**: O campo deve vir formatado como moeda Real e com precisão de 2 casas decimais. Ex.: (R$ 350,45);

- **<span id="rn-13">RN-13</span>**: O campo **_Valor Bruto_** é obrigatório e de preenchimento automático de acordo com o contrato do equipamento;
   - **<span id="rn-13-01">RN-13-01</span>**: Se o equipamento não possui contrato de ponto na obra o campo deve vir zerado (R$ 0,00);
   - **<span id="rn-13-02">RN-13-02</span>**: Em caso de Não Produção o campo deve vir zerado (R$ 0,00);
   - **<span id="rn-13-03">RN-13-03</span>**: Se o equipamento possui contrato por Hora o campo deve vir preenchido de acordo com a seguinte formula: (ValorUnitario x QuantidadeHoras);
   - **<span id="rn-13-04">RN-13-04</span>**: Se o equipamento possui contrato por Dia o campo deve vir preenchido com o mesmo valor do campo "Valor Unitário";
   - **<span id="rn-13-05">RN-13-05</span>**: Se o equipamento possui contrato por Mês o campo deve vir preenchido de acordo com a seguinte formula: (ValorUnitario / 30);
   - **<span id="rn-13-06">RN-13-06</span>**: Por ser um campo de preenchimento automático o mesmo deve estar sempre desabilitado e com a coloração cinza, de forma a diferenciar dos demais campos editáveis.
   - **<span id="rn-13-07">RN-13-07</span>**: O campo deve vir formatado como moeda Real e com precisão de 2 casas decimais. Ex.: (R$ 350,45);

- **<span id="rn-14">RN-14</span>**: O campo **_Valor Desconto_** é obrigatório e de preenchimento automático de acordo com o contrato do equipamento e com as informações de horas mecânicas contidas no lançamento;
   - **<span id="rn-14-01">RN-14-01</span>**: Se o equipamento não possui contrato de ponto na obra o campo deve vir zerado (R$ 0,00);
   - **<span id="rn-14-02">RN-14-02</span>**: SE não houver horas mecânicas lançadas o campo deve vir zerado (R$ 0,00);
   - **<span id="rn-14-03">RN-14-03</span>**: Se o equipamento possui contrato por Hora o campo deve vir zerado (R$ 0,00) pois o desconto será aplicado somente na Medição;
   - **<span id="rn-14-04">RN-14-04</span>**: Se o equipamento possui contrato por Dia ou por Mês o valor do campo deve ser calculado de acordo com a seguinte formula: ( (HoraEquivalente - HorasMecanicas) x (ValorBruto / HoraEquivalente) );
      - A hora equivalente é obtida no contrato.
   - **<span id="rn-14-05">RN-14-05</span>**: Por ser um campo de preenchimento automático o mesmo deve estar sempre desabilitado e com a coloração cinza, de forma a diferenciar dos demais campos editáveis.
   - **<span id="rn-14-06">RN-14-06</span>**: O campo deve vir formatado como moeda Real e com precisão de 2 casas decimais. Ex.: (R$ 350,45);

- **<span id="rn-15">RN-15</span>**: O campo **_Valor a Pagar_** é obrigatório e de preenchimento automático;
   - **<span id="rn-15-01">RN-15-01</span>**: O valor do campo é calculado de acordo com a seguinte formula (ValorBruto - ValorDesconto);
   - **<span id="rn-15-02">RN-15-02</span>**: Por ser um campo de preenchimento automático o mesmo deve estar sempre desabilitado e com a coloração cinza, de forma a diferenciar dos demais campos editáveis.
   - **<span id="rn-15-03">RN-15-03</span>**: O campo deve vir formatado como moeda Real e com precisão de 2 casas decimais. Ex.: (R$ 350,45);

- **<span id="rn-16">RN-16</span>**: O campo **_Observação_** é de preenchimento obrigatório somente em caso de "Não Produção";
   - **<span id="rn-16-01">RN-16-01</span>**: Um texto somente de espaços em branco não deve ser considerado como informação. Deve ser o equivalente a não informar nenhum caracter no campo;
   - **<span id="rn-16-02">RN-16-02</span>**: Caso seja informado o campo deve possuir pelo menos 5 carecteres, entendendo que nenhuma informação relevante pode ser descrita com menos texto que isso.

- **<span id="rn-17">RN-17</span>**: O campo **_Serviços_** é obrigatório quando o equipamento produziu no dia;
   - **<span id="rn-17-01">RN-17-01</span>**: No campo devem ser listados todos os serviços ativos na obra para o dia do ponto. Esta informação vem da Frente de Serviço na Obra;
   - **<span id="rn-17-02">RN-17-02</span>**: Deve ser possível informar mais de um serviço, desde que não informe o mesmo serviço mais de uma vez.

- **<span id="rn-18">RN-18</span>**: As **_Horas Mecânicas_** é uma lista de horas informadas correspondente aos horários em que o equipamento ficou parado para manutenção. Esta informação não é obrigatória;
   - **<span id="rn-18-01">RN-18-01</span>**: A lista deve estar sempre ordenada de forma crescente, ou seja, da menor hora para a maior;
   - **<span id="rn-18-02">RN-18-02</span>**: Não podem ser lançadas horas com período coincidindo (igual ou fazendo intersecção) com outras horas mecânicas já existentes na lista;
   - **<span id="rn-18-03">RN-18-03</span>**: A "Hora Final" deve ser sempre maior que a "Hora Inicial";
   - **<span id="rn-18-04">RN-18-04</span>**: As horas, tanto nos campos quanto na lista, devem estar formatadas em Hora e Minuto (HH:mm).

- **<span id="rn-19">RN-19</span>**: O campo **_Total de Horas_** é um campo gerado automaticamente devendo sempre estar desabilitado e na coloração cinza, de forma a diferenciar dos demais campos editáveis;
   - **<span id="rn-19-01">RN-19-01</span>**: Se não forem informadas horas mecânicas o campo deve estar zerado (00:00);
   - **<span id="rn-19-02">RN-19-02</span>**: Este campo deve ser o somatório das horas mecânicas lançadas. A fórmula para o cálculo é a seguinte:
$$
TotalDeHoras = \sum (horaFinal - HoraInicial)
$$

- **<span id="rn-20">RN-20</span>**: O campo **_Motivo da Não Produção_** é obrigatório somente para caso de "Não Produção";
   - **<span id="rn-20-01">RN-20-01</span>**: Somente uma das opções pode ser selecionada;
      - A disposição da Obra;
      - A disposição do Proprietário;
      - Folga de Pagamento;
      - Hora Mecânica

## 7.2 - Validações

//TODO:
