# GitConfigOptionsThatCanHelp
Alguns parâmetros para trabalhar com repositórios grandes, podem trazer melhoras em valores diametralmente diferentes, vale o teste.

As configurações podem ser adicionadas no contexto global `--global` ou na pasta do repositório.

## Para listar as configurações

```bash
git config --list
```
```bash
git config --list --global
```
```bash
git config --list --show-origin
```

## Para aplicar configurações

```bash
git config core.compression 9
git config http.postbuffer=524288000
git config core.fscache true
git config http.lowSpeedLimit 1
git config http.lowSpeedTime 999999
git config pack.deltaCacheSize 2048M
git config pack.threads 0
git config feature.manyFiles true
```
## Para remover configurações
```bash
git config --global --unset core.compression 9
```
```bash
git config --unset core.compression 9
```

# core.compression
Seta os valores para ambos core.loosecompression e pack.compression.
Nível de compressão, entre -1 a 9.
0 desabilita, 9 é o maior nível de compressão e -1 usa o padrão zlib.
Valor default é 1. Pode-se tentar variar entre os valores -1, 0 e 9 para ver qual ajuda a melhorar a performance.

# http.postbuffer
Tamanho máximo em bytes do buffer usado pelo smart HTTP quando fizer POST no sistema remoto. Default é 1MiB

# core.fscache
Com o cache habilitado os dados são lidos em volume a armazenados na memória para certas operações, trazendo um ganho de performance.
No manual do git 2.x não há mais referência dessa configuração, mas ao aplicar o git não da erro e aparece como configuração ativa, vale o teste.

# http.lowSpeedLimit e lowSpeedTime
Define um valor mínimo de transferência e por quanto tempo valores abaixo desse limite serão aceitos.
Caso a velocidade de transferência fique inferior ao limite estabelecido, por mais tempo que o limite estabelecido, o processo é encerrado.

# pack.deltaCacheSize
Tamanho máximo de memória (bytes) usado para cache antes de escrever num pacote. É usado para acelerar escrita de objetos. Fazer o repack de repositórios grandes em máqunas com pouca ram pode impactar no desempenho, principalmente se for usdo SWAP, então aumentar o valor pode ajudar no desempenho, mas também atrapalhar. O padrão é 256Mib, 0 significa infinito.

# pack.threads
Número de threads a serem gerados quando o processo busca pelas melhores correspondências de delta. Tem o objetivo de reduzir o empacotamente em processadores multicore. 0 signfica que o git auto detectará o melhor valor que considerar necessário, analisando a quantidade de CPU disponível. Também pode tentar forçar um valor diferente.

# feature.manyFiles
Habilita configuração para otimizar repositórios com muitos arquivos no diretório de trabalho. Comandos como `git status`, `git checkout` e `git add` podem ser mais lentos e essa configuração pode aumentar a performance.

# Garbage Collector
Faz limpeza de arquivos desnecerrários e otimiza o repositório local.
Geralmente o comando executa em poucos minutos, mas com a opção `--aggressive` o processo rodará pelo tempo q for necessário para realizar a melhor otimização.
```bash
git gc
```
```bash
git gc --aggressive
```

# LINKS INTERESSANTES
[GIT GC] (https://git-scm.com/docs/git-gc/2.43.0)

[Manaul GIT](https://www.git-scm.com/docs/git-config/2.14.6)

[Dicas de performance para GIT](https://www.git-tower.com/blog/git-performance/)
