# Trabalho TCP — Gerador de Música a partir de Texto

Projeto desenvolvido para a disciplina de **Técnicas de Construção de Programas (TCP)** na UFRGS. A aplicação converte entradas de texto (digitadas diretamente ou lidas de arquivos `.txt`) em sequências musicais utilizando a biblioteca **JFugue** e interface gráfica em **Java Swing**.

## Mapeamento de Caracteres

O texto de entrada é interpretado caractere por caractere para gerar a música:

| Caractere | Ação Musical |
| :--- | :--- |
| `A` a `G` (maiúsculas) | Toca a nota correspondente (Lá, Si, Dó, Ré, Mi, Fá, Sol) na oitava atual |
| `a` a `g` (minúsculas) / outros | Repete a nota anterior (se o caractere anterior for uma nota de `A` a `G`) ou faz uma pausa |
| Espaço (` `) | Dobra o volume atual (retorna ao volume padrão se ultrapassar o limite máximo) |
| Dígitos (`0`–`9`) | Altera o instrumento somando o dígito ao ID do instrumento atual |
| `?` | Aumenta uma oitava (retorna à oitava inicial ao atingir o limite) |
| `!` | Altera o instrumento para *Agogo* (ID 114) |
| `i`, `o`, `u` | Altera o instrumento para *Harpsichord* (ID 7) |
| Quebra de linha (`\n`) | Altera o instrumento para *Tubular Bells* (ID 15) |
| `;` | Altera o instrumento para *Pan Flute* (ID 76) |
| `,` | Altera o instrumento para *Church Organ* (ID 20) |

## Estrutura do Projeto

- `identificaCaractere.java` — Interpreta o texto de entrada e constrói a string de comandos musicais do JFugue.
- `ControlaSom.java` — Gerencia as configurações de reprodução (volume, instrumento MIDI e oitava).
- `Leitura.java` — Responsável pela abertura e leitura de arquivos de texto.
- `TelasPlayer/src/Telas/` — Telas da interface gráfica em Java Swing (`TelaPrincipal.java` e `TelaMusica.java`).
- `TelasPlayer/IconPlay.png` e `TelasPlayer/IconPause.png` — Ícones utilizados pelo reprodutor.
- `jfugue-5.0.9.jar` — Biblioteca JFugue utilizada para reprodução de áudio.

## Requisitos e Execução

- **Java JDK** (8 ou superior)
- Biblioteca `jfugue-5.0.9.jar` adicionada ao *classpath* do projeto.

Para compilar e executar via terminal na raiz do projeto:

```bash
javac -cp ".;jfugue-5.0.9.jar" ControlaSom.java identificaCaractere.java Leitura.java TelasPlayer/src/Telas/*.java
java -cp ".;jfugue-5.0.9.jar;TelasPlayer/src" Telas.TelaPrincipal
```
