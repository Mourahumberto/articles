# I/O Manegement

Quando iremos mensurar a performace do disco precisamos levar em conta alguns indicadores.
-> Utilization: è a porcentagem em que o disco está processando I/O em porcentagem%
-> Saturação: Refere-se o quão ocupado o disco está de processamento de I/O, significa que tem um gargálo de desempenho
e quando essa saturação é 100%, o disco não aceita novas solicitações de I/O
-> IOPS (Input/Output Per Second): Referece ao número de I/O request por segundo.
-> Throughput: O tamanho de I/O request por segundo
-> Response time: referese ao tempo entre o envio de um I/O request e o recebimento do Response

Usando o comando iostat para verificar os indicadores do disco

$ iostat -d -p sda -x 1
```
Device            r/s     rkB/s   rrqm/s  %rrqm r_await rareq-sz     w/s     wkB/s   wrqm/s  %wrqm w_await wareq-sz     d/s     dkB/s   drqm/s  %drqm d_await dareq-sz     f/s f_await  aqu-sz  %util
sda              0,00      0,00     0,00   0,00    0,00     0,00    0,00      0,00     0,00   0,00    0,00     0,00    0,00      0,00     0,00   0,00    0,00     0,00    0,00    0,00    0,00   0,00
sda1             0,00      0,00     0,00   0,00    0,00     0,00    0,00      0,00     0,00   0,00    0,00     0,00    0,00      0,00     0,00   0,00    0,00     0,00    0,00    0,00    0,00   0,00
sda2             0,00      0,00     0,00   0,00    0,00     0,00    0,00      0,00     0,00   0,00    0,00     0,00    0,00      0,00     0,00   0,00    0,00     0,00    0,00    0,00    0,00   0,00
sda3             0,00      0,00     0,00   0,00    0,00     0,00    0,00      0,00     0,00   0,00    0,00     0,00    0,00      0,00     0,00   0,00    0,00     0,00    0,00    0,00    0,00   0,00
 ```

- \%util é o uso de disco
- r/s + w/s é o iops IOPS
- rkB/s + wkB/s is the throughput
- r_await + w_await is the response time

$ iostat
```
avg-cpu:  %user   %nice %system %iowait  %steal   %idle
           1,56    0,01    0,49    0,04    0,00   97,91
```

- %idle tempo que a CPU está ociosa
- %iowait porcentagem do tempo que o cpu espera para receber resposta de I/O

Observação dos processos de I/O.
- com o iostat você consegue ver as estatiscas do disco. Porém você não vê quais processos estão consumindo mais recursos de I/O.

- mas pode ser visto com pidstat e iotop
```
$ pidstat -d 1
13:39:51      UID       PID   kB_rd/s   kB_wr/s kB_ccwr/s iodelay  Command 
13:39:52      102       916      0.00      4.00      0.00       0  rsyslogd
```

- User ID (UID) and Process ID (PID).
- The size of data read per second (kB_rd/s), in KB.
- The size of the write request data issued per second (kB_wr/s), the unit is KB.
- The data size of canceled write requests per second (kB_ccwr/s), in KB.
- Block I/O delay (iodelay), including the time to wait for the completion of synchronized block I/O and swap-in block I/O, in clock cycles.
```
$ sar -p -d -b 1
```

# SOCKETS

- Sockets são a maneira na qual um processo consegue se comunicar com outro no mesmo servidor ou em servidores distintos.
Um endereço de socker é a combinação de um protolo TCP ou UDP um endereço de IP e uma porta, algo parecido com isso "203.0.80,1:443" Neste exemplo temos
algo que pode ser um servidor web com HTTPS. 
- Cada servidor tem apenas um socket com a mesma numeração exemplo, se rodamos uma aplicação em uma porta 9090, não conseguiriamos rodar outra aplicação rodar,
na porta 9090 neste mesmo servidor, a não ser com redirect usando docker, mas esse é outro assunto. 
- nas conexões de sockets o cliente também abre sockets para se comunicar. Um exemplo se vamos nos conectar a um servidor web, de aplicação ou até ssh nosso cliente
também abre uma porta para se conectar a porta 80 do servidor.

- Comandos para verificar as portas usadas nos processos 
$ ss


# Network Conceitos
Entendo Ips privados e públicos
```
Privados
10.0.0.0 -10.255.255.255 (/8)

172.16.0.0 - 172.31.255.255 (/12)

192.168.0.0 -192.168.255.255 (/16)
```

- Comandos em linux para rede.
```
$ ip a 
$ ip addr
para ter mais informações das interfaces de rede 
```

## Load Average 
```
Com o comando htop ou uptime podemos retirar essa métrica
load average: 0,80, 2,00, 5,30
```
isso significa que nos ultimo 1 minuto os processos tiveram uma média de menos que 1 core.
O segundo número diz que nos ultimos 5 minutos teve um uso de 2 cores e no ultimos 15 min. um uso de 5.3 cores.
O load Avarege mede a média de uso de cpu's neste caso se fosse um servidor com 8 cpu's estaria com pouco uso. Porém se fosse com 4 cpu's
nos ultimos 15 minutos ele estaria comum alto processamento e uma lentidão nos processos. Porém nos ultimos 5 minutos estaria com um uso adequado.
