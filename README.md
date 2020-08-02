
# Oracle Webinar: Como fazer um bom Design de código em Java

### JAVA 25 ANOS

# 12 Fatores para um bom design

- O porquê do design.

- Boas práticas para Orientação a Objetos

- Effective Java nos métodos

- Divisão de camadas

- Estrutura de pacotes

- Exceções

- Over Engineering

- Qualidade em Testes

- Code Style e Ferramentas de análise estática

- Pair Programming

- Code Review e Pull Request

- Documentação e Configuração

## 1. O porquê do Design

- Modificações com :
	- Facilidade
	- Segurança

- Evolução com:
	- Menor investimento

**JCP** : Decisões que foram tomadas ao longo dos anos e sobre como o uso de **especificações** permitiu que não houvesse **vendor lock-in** com bibliotecas e apis no ecossistema Java.

## 2. Boas práticas para Orientação a Objetos

### Pequenas Grandes Ações

**Nomes** : Não economize com o tamanho do nome, desde que ele descreva bem o propósito do que está no método, variável, classe, etc.

**Getters e Setters** : Frameworks usam a api de Reflection para executar parse de dados, então não é necessário que você crie eles até mesmo para objetos anêmicos, se não for necessário.

**ENUM** : Use enums no lugar de constantes, isso permite deixa o código mais limpo. Além disso, Enums podem ser classes bem ricas e podem facilitar muito a implementação de alguns padrões de projeto.

###  Programe voltado a interface

- Má prática :
``` java
public ArrayList<Project> consultList(
	Pageable pageagle, String language) {
	return projectRepository
		.findByLanguage(language, pageable);
}
```
- Boa prática :
``` java
public List<Project> consultList(
	Pageable pageagle, String language) {
	return projectRepository
		.findByLanguage(language, pageable);
}
```
### Evite herança, favoreça composição

#### Herança
- :x: Encapsulamento fraco
- :x: Acoplamento forte
- :x: Alteração na superclasse impacta nas subclasses
- :x: Não permite mudança de comportamento em tempo de execução

#### Composição
- :heavy_check_mark: Permite definir comportamentos complexos.
- :heavy_check_mark: Comportamentos diferentes em runtime.
- :heavy_check_mark: Melhor encapsulamento.

**Herança**
Voluntário é uma Pessoa
```java
@Entity
public class Voluntary extends Person {

	@Id
	@GeneratedValue(strategy = GenerationType.IDENTITY)
	private Long id;

	@NotBlank
	@Enumerated(EnumType.STRING)
	List<LanguagemEnum> interests;
	
}
```

**Composição**
Projeto tem um Responsável
```java
public class Project {

	@Id
	@GeneratedValue(strategy = GenerationType.IDENTITY)
	private Long id;

	@NotBlank
	private String name;

	@NotBlank
	@Enumerated(EnumType.STRING)
	private LanguagemEnum language;

	@NotBlank
	private Person responsible;

}
```

### Favoreça imutabilidade e simplicidade

- **forma =** :small_red_triangle:
- **forma =** :red_circle:

:warning:**forma é mutável**:warning:

### Exemplo 01 :
![class String](https://user-images.githubusercontent.com/56324728/89113473-e4866180-d447-11ea-8c51-52804dc46f93.jpg)

### Exemplo 02 :
![image](https://user-images.githubusercontent.com/56324728/89113481-f8ca5e80-d447-11ea-9ebf-1985f705851c.png)

:arrow_right: Nesse caso, quando for criada uma classe que é imutável e o parametro dela usar objetos que são mutáveis, ou seja, que permitem que sejam alterados uma vez que forem instanciados, *o ideal  é,  se você for fazer um get por exemplo, não devolva o __this.responsible__, devolva uma cópia desse objeto e __não__ ele, uma referência dele, pois assim você garante que ninguém estará mudando o que compõe o seu objeto.*

### Outro exemplo :
![image](https://user-images.githubusercontent.com/56324728/89113584-632fce80-d449-11ea-9bce-2271b0dc3aba.png)

## 3. Effective Java nos Métodos

![image](https://user-images.githubusercontent.com/56324728/89113607-d89b9f00-d449-11ea-8fb0-50f3f044d7c8.png)

## 4. Divisão de Camadas
![image](https://user-images.githubusercontent.com/56324728/89113691-99218280-d44a-11ea-9c1d-7b9e705c5ed4.png)

## 5. Estrutura de Pacotes

### Package By Layer
![image](https://user-images.githubusercontent.com/56324728/89113729-00d7cd80-d44b-11ea-95a9-3f3fe60620b2.png)

### Package By Feature
![image](https://user-images.githubusercontent.com/56324728/89113762-76439e00-d44b-11ea-8700-5b52200f2f89.png)

## 6. Exceptions

### Verificadas
![image](https://user-images.githubusercontent.com/56324728/89113805-e5b98d80-d44b-11ea-8ebe-bffb53e40316.png)

### Não Verificadas
![image](https://user-images.githubusercontent.com/56324728/89113854-8019d100-d44c-11ea-9f26-383c0e2fed1c.png)

## 7. Over Engineering

### O que é?
![image](https://user-images.githubusercontent.com/56324728/89113874-c3743f80-d44c-11ea-81bf-32b06b6c857a.png)

### Princípios
![image](https://user-images.githubusercontent.com/56324728/89113891-e43c9500-d44c-11ea-9f35-0adace767d6c.png)

### Exemplo do que NÃO fazer
![image](https://user-images.githubusercontent.com/56324728/89113930-54e3b180-d44d-11ea-8634-deedcbe6cfe1.png)

## 8. Qualidade em Testes

### Passar o teste não significa que você tem qualidade
![image](https://user-images.githubusercontent.com/56324728/89113943-93796c00-d44d-11ea-9be4-9841355816a9.png)

### Pirâmide de Testes
![image](https://user-images.githubusercontent.com/56324728/89113973-e9e6aa80-d44d-11ea-9d5f-2dd68b8ba8c1.png)

## 9. Code Style e Ferramentas de análise estática

### Code Style
![image](https://user-images.githubusercontent.com/56324728/89114034-ae001500-d44e-11ea-9aed-743cdceb50f7.png)

### Itens do Code Style do Twitter
![image](https://user-images.githubusercontent.com/56324728/89114061-f0295680-d44e-11ea-8892-864b1a6d1732.png)

### Ferramentas de análise estática
![image](https://user-images.githubusercontent.com/56324728/89114075-0fc07f00-d44f-11ea-9353-51f9fd4124c6.png)

## 10. Pair Programming

![image](https://user-images.githubusercontent.com/56324728/89114123-662dbd80-d44f-11ea-8f9f-8aec6841d2d2.png)

### O que fazer para ter um bom Pair Programming?
![image](https://user-images.githubusercontent.com/56324728/89114147-a2f9b480-d44f-11ea-9780-99554c18d4bb.png)

### O que NÃO fazer
![image](https://user-images.githubusercontent.com/56324728/89114160-c4f33700-d44f-11ea-9e37-3b121ba681fb.png)

## 11. Code Review e Pull Request

### Pull Request
![image](https://user-images.githubusercontent.com/56324728/89114205-24514700-d450-11ea-8b31-28f17af5c7d0.png)

### Code Review
![image](https://user-images.githubusercontent.com/56324728/89114225-5793d600-d450-11ea-9205-e93ec8032fc2.png)

 ### O que analisar?
![image](https://user-images.githubusercontent.com/56324728/89114261-c2dda800-d450-11ea-8861-1ae334769c8d.png)

### Comentários
![image](https://user-images.githubusercontent.com/56324728/89114267-e56fc100-d450-11ea-95e0-191371b96099.png)

## 12. Documentação e Configuração

![image](https://user-images.githubusercontent.com/56324728/89114284-06381680-d451-11ea-93d3-0fd0b69864c3.png)

### Exemplo de um README
![image](https://user-images.githubusercontent.com/56324728/89114303-50b99300-d451-11ea-90bb-26ea0f438202.png)

## [Link](https://javabahia.github.io/como-fazer-um-bom-design-codigo-em-java/) com mais detalhes sobre a palestra, escrito pela  @psanrosa13
