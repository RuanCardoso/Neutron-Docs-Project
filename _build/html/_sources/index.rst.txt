.. role:: raw-html(raw)
    :format: html

********************
Neutron
********************
*Neutron é um framework de rede ClientSide e ServerSide para a engine Unity, é usado criar jogos multijogador simples e avançados, tem um sistema de Matchmaking flexível que coloca seus jogadores em salas, canais e grupos.* :raw-html:`<br/>`
*Neutron tem um alto poder de customização ao lado do cliente ou servidor, é orientado a eventos e pode fazer oque você quiser utilizando seu alto poder de customização.* :raw-html:`<br/>`
*Neutron é multi-threading e busca sempre antigir alta performance, baixo consumo de banda e baixo nível de alocações no GC, não possui limites de Ccu, possui 3 protocolos que podem ser usados simultaneamente, TCP, UDP E RUDP(Reliable Udp).* :raw-html:`<br/>`

.. note:: *Neutron utiliza reflexão para encontrar os metódos no Awake, que possui um baixo custo pois é executado somente uma vez, os metódos são invocados via delegados(delegates) para alta performance.*
.. note:: *Neutron não busca assets e não marca assets com Guid, os objetos são identificados por um Id(NeutronView) que é armazenado em um dicionário para alta performance.*
.. note:: *Neutron está em ativo desenvolvimento e nosso objetivo é sempre manter o maior nível possível de performance e o menor consumo de banda possível, sem esquecer das alocações no GC (;*
.. warning:: *Esta documentação leva em consideração que você saiba o básico da linguagem C# e da Unity Engine.*
.. note:: *Suporte, Relato de Bugs, ou Contato Pessoal, envie um email para:* neutron050322@gmail.com
.. note:: *Para contribuir com o projeto. Para transferências nacional, Brasil(Pix):* **0000-0000-00000**, *para Internacional(Paypal):* ruan@gmail.com

*Este é um breve resumo, para saber do que Neutron é capaz, continue lendo....*

Log de Mudanças
===========================
*Versão 2.0(Beta) - Atual*
---------------------------
- *gRPC*
- *iRPC*
- *SyncVar*
- *Auto Synchronization*
- *Matchmaking*
- *Custom Packets*
- *etc..*

*Versão 1.0(Alpha)*
---------------------------
- *Lançamento do Neutron.*

Problemas Conhecidos
===========================
- Sem problemas encontrados.

.. toctree::
   :caption: Neutron Framework
   :maxdepth: 2
   :hidden:

   Pages/starting
   Pages/rpc