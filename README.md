# NLP_processo_compras
Analisador de processo de compras

Colegas,

Essa semana eu fiz aqui um código pra me ajudar nas análises dos processos de compras, coisa que eu preciso fazer com muita frequência na SAMS.

Como utilizei bastante a biblioteca nltk e tokenização, além de regex, repasso pra vocês analisarem se ele pode servir como entrega da disciplina de PLN.

Caso vocês achem que pode servir, acho que Sanderson teria que dar uma boa melhorada no código. Se acharem que não é suficiente para usarmos como entrega da disciplina de PLN, pode deixar o código como está que já está me servindo.

O código tem por objetivo tratar as seguintes situações:

Situação (1)

Nos processos de compra, depois que acontece a licitação a DG homologa os itens que tiveram sucesso na licitação e a COFIN emite as Notas de Empenho para cada um dos fornecedores.
O processo então volta para mim para que eu envie por e-mail as Notas de Empenho a cada um dos fornecedores vitoriosos na licitação.

Para atender a essa demanda, criei o “Objetivo 1: Construir as mensagens dos emails para envio das notas de empenho”.

Para isso o código procura dentro do processo os e-mails de cada fornecedor, seus nomes e números de nota de empenho e cria um texto padrão de e-mail, personalizado para cada fornecedor, salvando esse texto em um arquivo chamado “textos_emails.txt”. Optei pela criação do txt ao invés do envio automático do e-mail porque eu prefiro conferir cada e-mail antes deles serem enviados.

Para esse objetivo 1, configurei o código para buscar apenas na parte do processo anterior aos envios dos e-mails. Porque eu estou usando um processo completo para testar o código (no qual eu já enviei os e-mails), e na situação real o processo não estará completo. Se eu não limitasse a busca a esse ponto do processo o código estaria buscando os e-mails nos próprios e-mails que eu enviei nesse processo específico.

Situação (2)

Nos processos de compras, é necessário identificar quais foram os itens que não tiveram sucesso na licitação (desertos ou fracassados) para que se possa iniciar o quanto antes um novo processo de aquisição de modo que que dê tempo desse segundo processo ser concluído ainda no mesmo exercício financeiro. Além disso, é necessário checar se todos os produtos que tiveram sucesso na licitação estão incluídos em alguma Nota de Empenho, porque se não tiver, o fornecedor não receberá o e-mail e não entregará o produto.


Para essa demanda, foi estabelecido o “Objetivo 2: Listar os produtos fracassados e checar se todos os produtos homologados pela DG constam nas notas de empenho anexadas ao processo”.

Para isso, o código gera duas listas, a lista “produtos_homologados” e a lista “produtos_homologados_nao_presentes_nas_NE”. 
A lista “produtos_homologados_nao_presentes_nas_NE”, em um processo onde tudo está correto é para estar vazia, mas às vezes não está, como nesse processo específico. Essa verificação é uma coisa muito trabalhosa para detectar sem automação e muito importante porque a COFIN precisa ser avisada para verificar onde está o erro o quanto antes.

Situação (3)

Depois que as Notas de Empenho são enviadas para as empresas fornecedoras é necessário acompanhar as entregas para ir dando baixa nas entregas e enviar as Notas Ficais à SEMAT para pagamento. Para isso é interessante ter uma planilha, que eu chamei de 'Planilha de Controle de Entregas.xlsx', que o código está gerando, com as informações de número da Nota de Empenho, nome do fornecedor, valor da nota de empenho, e-mail do fornecedor (porque quando a entrega atrasa temos que ficar enviando e-mails cobrando, e isso é muito frequente) além de algumas células em branco para serem preenchidas à medida em que as entregas vão sendo feitas.

Para essa demanda foi estabelecido o “Objetivo 3: Criar uma Planilha para acompanhamento das entregas dos produtos pelos fornecedores”.

A criação da planilha foi colocada dentro de um if-else porque só faz sentido criar essa planilha depois do envio das notas de empenho, e o código pode ser usado para outras finalidades antes da necessidade da criação dessa planilha.

Situação (4)

Por último, como o processo fica sendo tramitado para pagamento e voltando para a SAMS a cada entrega de cada fornecedor, e dezenas de páginas são anexadas ao processo a cada ida e vinda dessa, é muito fácil perder o controle se todos os pagamentos já foram feitos. Se já foram, o processo pode ser arquivado, se não foram, não pode ainda.

Por isso foi criado o “Objetivo 4: Checar se todos os pagamentos aos fornecedores já foram feitos para poder arquivar o processo”.

Essa funcionalidade gera a planilha 'Planilha de Controle de Pagamentos.xlsx' com a adição da coluna Data_Pag com as datas dos pagamentos de cada um dos fornecedores, caso esse pagamento tenha sido feito e “Não” caso ainda não tenha.

O processo usado para testar o código está aqui: https://drive.google.com/file/d/1pQB3RbkuaEy-0w55V07zoH0Z4byEODfT/view?usp=sharing
