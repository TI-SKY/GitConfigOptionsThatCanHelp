# GitConfigOptionsThatCanHelp
Alguns parâmetros para trabalhar com repositórios grandes

As configurações podem ser adicionadas no contexto global ou na pasta do repositório.

```bash
git config --global core.compression 9
git config --global http.keepalive=true
git config --global http.postbuffer=524288000
git config --global core.fscache=true
git config --global http.lowSpeedLimit 1
git config --global http.lowSpeedTime 999999
git config --global pack.deltaCacheSize 2048M
git config --global pack.threads 0
```

# core.compression
Nível de compressão, entre -1 a 9.
0 desabilita, 9 é o maior nível de compressão e -1 usa o padrão zlib.
Valor default é 1. Pode-se tentar varias entre os valores -1, 0 e 9 para ver qual ajuda a melhorar a performance.

# http.keepalive

# http.postbuffer
Tamanho máximo em bytes do buffer usado pelo smart HTTP quando fizer POST no sistema remoto. Default é 1MiB

# http.lowSpeedLimit e lowSpeedTime
Define um valor mínimo de transferência e por quanto tempo valores abaixo desse limite serão aceitos.
Caso a velocidade de transferência fique inferior ao limite estabelecido, por mais tempo que o limite estabelecido, o processo é encerrado.

# pack.deltaCacheSize
Tamanho máximo de memória (bytes) usado para cache antes de escrever num pacote. É usado para acelerar escrita de objetos. Fazer o repack de repositórios grandes em máqunas com pouca ram pode impactar no desempenho, principalmente se for usdo SWAP, então aumentar o valor pode ajudar no desempenho, mas também atrapalhar. O padrão é 256Mib, 0 significa infinito.

# pack.threads
Números de threads a serem gerados quando o processo busca pelas melhores correspondências de delta. Tem o objetivo de reduzir o empacotamente em processadores multicore. 0 signfica que o git auto detectará o melhor valor que considerar necessário, analisando a quantidade de CPU disponível. Também pode tentar forçar um valor diferente.


# LINKS INTERESSANTES

[Manaul GIT](https://www.git-scm.com/docs/git-config/2.14.6)

[Dicas de performance para GIT](https://www.git-tower.com/blog/git-performance/)
