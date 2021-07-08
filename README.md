---- Validação 1

select concat(t.stone_rti,cast(t.data_transacao as date)) as chave, count(*) as contagem from transacao t
where t.status in (10,22) and t.data_transacao::date > '2018-01-01' and t.stone_rti not in ('')
group by chave
having count(*) > 1;

---- Validação 2

select concat(t.stone_rti,racc.codigo_autorizacao) as chave, count(*) as contagem, t.data_transacao from transacao t
inner join retorno_aprovacao_cartao_credito racc on t.id = racc.transacao_id
where t.status in (10,22) and t.data_transacao::date > '2018-01-01' and t.stone_rti not in ('')
group by chave, t.data_transacao 
having count(*) > 1;
