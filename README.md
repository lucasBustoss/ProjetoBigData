
# Projeto Ingresso RockinRio

A imagem do projeto no repositório representa o fluxo da aplicação, ou seja, como ela deve funcionar em produção. Entretanto, neste README, vou explicar alguns detalhes técnicos que podem ser implementados para a melhor experiência do usuário. 



## Sistema de filas

É importante ter um sistema de fila que controla a entrada no portal para seleção de ingressos, que respeite a ordem de chegada de cada pessoa no site. O sistema, além de diminuir a ansiedade do usuário, apresentando as informações de quando será a vez dele, pode também diminuir a quantidade de atualizações na página, evitando qualquer tipo de sobrecarga no servidor. Vale ressaltar que o sistema de filas deve se manter inalterável mediante atualizações ou queda da conexão. Ou seja, a pessoa que pegou um lugar na fila deve manter esse lugar até que a mesma acesse o portal. Essa tela deve ser atualizada automaticamente de tempos em tempos com a situação da fila.


## Middeware validaEstoque

O middleware validaEstoque deve ser chamado em 2 pontos: Ao acessar a primeira vez o portal e ao selecionar e confirmar os ingressos, para direcionar para a tela de pagamento. Dessa forma, conseguimos controlar o recebimento dos ingressos mediante a disponibilidade. Podemos também implementar uma terceira chamada, na tela de filas, para apresentar aos usuários se ainda existem ou não ingressos disponíveis. 

## Sessão

Uma vez que chega a vez do usuário e existam ingressos, deve-se abrir uma seção para o usuário com tempo limite de 15 minutos. Esse tempo garante que a pessoa não terá o ingresso reservado por um longo tempo, dando a possibilidade de retornarem ingressos para comercialização.

## Reserva de ingressos

Uma vez selecionados, confirmados e validados, os ingressos devem ser reservados para aquela sessão e não devem mais contar em estoque. Os ingressos só voltarão a ficar disponívels em caso de cancelamento do pagamento ou de expiração do tempo limite da sessão.

## Pagamento e confirmação

Com o pagamento confirmado, os ingressos serão atribuidos ao usuário logado e não estarão mais disponiveis para comercialização em nenhuma hipótese. Neste ponto, podemos avaliar também a implementação de um load balancer, para evitar que usuários sofram com gargalos decorrentes à sobrecarga nos servidores de pagamento. 
