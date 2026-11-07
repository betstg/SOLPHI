# Guia pra IA cadastrar nas Infos do SOLPHI

Esta página é a biblioteca do mundo do livro SOLPHI. Quem usa são a Betty e o Harry. Se eles pedirem pra você cadastrar ou editar alguma coisa, siga este guia.

## Jeito 1, pelo navegador

Abra betstg.github.io/SOLPHI/infos/ e clique em "Novo". Escolha a Pasta, e se for personagem escolha também o Grupo. Preencha Nome, Resumo em uma linha, Detalhes e Tags, e clique em Salvar. A capa e a galeria aceitam imagem do computador.

## Jeito 2, direto no banco

O banco é um Supabase com acesso aberto, sem login. Toda chamada leva o cabeçalho `apikey`.

```
URL     https://mqrlnaygwuwthovepvyj.supabase.co/rest/v1/solphi_infos
apikey  sb_publishable_v4YPPXXPR0Vkue4IZ1gG7w_m16E0460
```

Ler tudo

```
curl "https://mqrlnaygwuwthovepvyj.supabase.co/rest/v1/solphi_infos?select=*" -H "apikey: sb_publishable_v4YPPXXPR0Vkue4IZ1gG7w_m16E0460"
```

Cadastrar um registro novo

```
curl -X POST "https://mqrlnaygwuwthovepvyj.supabase.co/rest/v1/solphi_infos" \
  -H "apikey: sb_publishable_v4YPPXXPR0Vkue4IZ1gG7w_m16E0460" \
  -H "Content-Type: application/json" \
  -d '{"tipo":"personagem","nome":"Nome","resumo":"Uma linha","detalhes":"Texto.\n\nOutro parágrafo.","tags":"npc lux guilda-x","imagem":"","galeria":[],"fonte":"biblia"}'
```

Editar um registro existente usa PATCH com `?id=eq.<id>` no fim da URL e só os campos que mudam. Apagar usa DELETE com o mesmo filtro. Antes de cadastrar, leia a lista e confira se o nome já existe, pra não duplicar.

## Campos

- `tipo` é a pasta. Valores aceitos `personagem`, `lugar`, `cla` (Clãs de Elysium), `guilda` (Guildas da LUX), `criatura` (Bestiário), `item`, `poder` (Poderes do CRUD), `tecnica`, `simbolo`, `regra`, `giria`, `evento` (Linha do tempo)
- `nome` é o nome canon, sem sobrenome (ninguém no mundo tem sobrenome)
- `resumo` é uma frase curta que aparece no card
- `detalhes` é o texto completo. Parágrafos separados por uma linha em branco (`\n\n`)
- `tags` são palavras separadas por espaço, sem acento de preferência
- `imagem` é a URL da capa. `galeria` é uma lista `[{"src":"url","legenda":"texto"}]`
- `fonte` é `biblia` pro que vem do livro e `fables` pro que veio do Friends and Fables

## Grupo dos personagens

O grupo de cada personagem vem das tags.

- Principal leva a tag `principal`
- NPC leva a tag `npc` mais a área, `arc`, `lux` ou `elysium`

Exemplo de NPC da LUX com tags `npc lux karas`.

## Regras do mundo pra respeitar

- Só cadastre o que está decidido na bíblia ou o que a Betty ou o Harry mandaram. Nome novo inventado só entra se eles aprovarem
- Ninguém tem sobrenome
- A palavra Veil não existe no SOLPHI
- Não escreva nome dos autores nos textos do mundo
