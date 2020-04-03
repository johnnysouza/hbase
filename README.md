# Atividade Prática – HBase

## Exercício 1

Agora, de dentro da imagem faça os sefuintes procedimentos:

- 1.Crie a tabela com 2 famílias de colunas: 
  - a.personal-data
  - b.professional-data
    - <code> create 'italians', 'personal-data', 'professional-data' </code>
  
- 2.Importe o arquivovia linha de comando
  - <code> hbase shell /tmp/italians.txt </code>

Agora execute as seguintes operações:

- 1.Adicione mais 2 italianos mantendo adicionando informações como data de nascimento nas informações pessoais e um atributo de anos de experiência nas informações profissionais;
  - <code> put 'italians', '11', 'personal-data:name',  'Tony Monatana'
put 'italians', '11', 'personal-data:city',  'Miami'
put 'italians', '11', 'personal-data:birthdate',  '20-04-1958'
put 'italians', '11', 'professional-data:role',  'Profissional liberal'
put 'italians', '11', 'professional-data:years',  '3' </code>
  - <code> put 'italians', '12', 'personal-data:name',  'Valentino Rossi'
put 'italians', '12', 'personal-data:city',  'Urbino'
put 'italians', '12', 'personal-data:birthdate',  '16-02-1979'
put 'italians', '12', 'professional-data:role',  'Piloto de motociclismo'
put 'italians', '12', 'professional-data:years',  '24' </code>

- 2.Adicione o controle de 5 versões na tabela de dados pessoais.
  - <code> alter 'italians', NAME => 'personal-data', VERSIONS => 5 </code>

- 3.Faça 5 alterações em um dos italianos;
  - <code> put 'italians', '11', 'personal-data:name',  'Leonardo Da Vinvi'
put 'italians', '11', 'personal-data:city',  'Vinci'
put 'italians', '11', 'personal-data:birthdate',  '15-04-1452'
put 'italians', '11', 'professional-data:role',  'Pintor/Escultor'
put 'italians', '11', 'professional-data:years',  '37' </code>

- 4.Com o operador get, verifique como o HBase armazenou o histórico.
  - <code> get 'italians', '11',{COLUMN=>'personal-data:name',VERSIONS=>2} </code>

- 5.Utilize o scan para mostrar apenas o nome e profissão dos italianos.
  - <code> scan 'italians',{COLUMNS=>['personal-data:name','professional-data:role']} </code>

- 6.Apague os italianos com row id ímpar
  - <code> deleteall 'italians', ['1', '3', '5','7','9','11'] </code>

- 7.Crie um contador de idade 55 para o italiano de row id 5
  - <code> incr 'italians', '5', 'personal-data:age', 55 </code>

- 8.Incremente a idade do italiano em 1
  - <code> incr 'italians', '5', 'personal-data:age' </code>
