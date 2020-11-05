# Mod11_ValidaCPF_CNPJ
> Realiza a validação do digito e algumas outras checagens especificas para CPF e CNPJ. 

Conjunto de procedimentos Genexus que permite a validação de qualquer digito gerado com base no Módulo 11, os procedimentos específicos para CPF e CNPJ implementam outras validações além do digito verificador.


## Procedure [Valida_CNPJ]
- Valida o digito verificador.
- Critica os CNPJ que contenha os 8 dígitos de sua base repetidos, desde que diferentes de zeros.
- Critica se a ordem do CNPJ é 0000, a ordem do CNPJ é utilizada para definir filiais e afins, e sempre inicia na primeira empresa com 1.
- Critica se as três primeiras posições do CNPJ for 000 e a quantidade de filiais maior que 300 desde que a base seja diferente de 00.0000.000

## Procedure [Valida_CPF]
- Valida o digito verificador.
- Critica todo CPF que contenha os 9 dígitos de sua base repetidos (Ex.: 222.222.222 ou 888.888.888)
- Por default também critica os CPF onde os 8 primeiros digito da base são repetidos, porém como existem algumas situações onde há instrução normativa para a utilização destes CPFs eles foram inseridos em uma lista e podem facilmente ser removidos conforme necessidade do seu negócio.
Observe que a lista contempla apenas a base (Sem os dígitos) sendo assim se o seu sistema atende alguma instrução normativa que aceite um ou mais destes CPFs basta remove los da lista, por exemplo:<br>
Para aceitar o CPF 000.000.001-91 remova da lista o valor 000000001<br>
Para aceitar o CPF 000.000.005-15 remova da lista o valor 000000005

## Procedure [Calcula_Mod11]
- Permite a validação de todo e qualquer código que utilize o algoritmo Mod11 para composição dos dígitos.
Ao utilizar este procedimento é preciso se atentar a 3 parâmetros (Base, Corte e Substituto), eles são necessários para que a procedure possa atende a diferentes situações, estas informações deveram ser obtidas junto a fonte do código a ser validado.<br>
Por exemplo:<br>
Para validar um CPF a base é 11, os Cortes são 0 e 1 e o Substituto é 0<br>
Para validar um CNPJ a base é 9, os Cortes são 0 e 1 e o Substituto é 0<br>
Para validar uma Conta do Banco do Brasil a base é 4, o corte é 0 e o substituto é X<br>

## Instalação

Genexus 16 ou Superior:

```Oxygene
1 - Na IDE Genexus, navegue em Knowledge Manager / Import.
2 - Selecione o Arquivo ValidaCPF_CNPJ.xml ** Note que é preciso alterar o filtro da caixa de seleção para XML.

```

## Exemplo de uso

```
Event 'Validar Digito CPF'
	
	If Valida_CPF.Udp(&CPF)
		
		Msg('CPF Válido')
		
	Else
		
		Msg('CPF Inválido')
		
	EndIf
	
Endevent

Event 'Validar Digito CNPJ'
	
	If Valida_CNPJ.Udp(&CNPJ)
		
		Msg('CNPJ Válido')
		
	Else
		
		Msg('CNPJ Inválido')
		
	EndIf
	
Endevent

Event 'Validar Formato CPF'
	
	If &CPF.IsMatch(ExpressaoRegular.CPF)
		
		Msg('Formato CPF Válido')
		
	Else
		
		Msg('Formato CPF Inválido')
		
	EndIf
	
EndEvent

Event 'Validar Formato CNPJ'
	
	If &CNPJ.IsMatch(ExpressaoRegular.CNPJ)
		
		Msg('Formato CNPJ Válido')
		
	Else
		
		Msg('Formato CNPJ Inválido')
		
	EndIf	
	
EndEvent
	
```

## Histórico de lançamentos

* 0.1.2
    * Primeira versão funcional [@gtorrezani](https://github.com/gtorrezani)
    * Correção aplicada nos valores de cortes em (14/10/2020 13:58)
    * Inclusão de exemplos sobre como Validar os Formatos. (05/11/2020 10:09)
    * Correção (Exclusão de parâmetros não utilizados na Proc que Calcula o Módulo 11) (05/11/2020 10:09)


## Meta

Gustavo Torrezani Matias – [@instagram](https://www.instagram.com/matiassolucoes/)

Distribuído sob a licença [MIT](https://choosealicense.com/licenses/mit/)
