## Ativar firewall customizado

```
sudo ufw enable
```

## Desativar firewall customizado

```
sudo ufw disable
```

## Liberar portas

```
sudo ufw allow ${numero_porta}/tcp
```

## Verificar portas liberadas

```
sudo ufw status numbered
```

### exemplo resultado

```
  [ 1] 3000/tcp ALLOW IN Anywhere
  [ 2] 3002/tcp ALLOW IN Anywhere
  [ 3] 5000/tcp ALLOW IN Anywhere
  [ 4] 139/tcp ALLOW IN Anywhere
  [ 5] 445/tcp ALLOW IN Anywhere
  [ 6] 137/tcp ALLOW IN Anywhere
  [ 7] 138/tcp ALLOW IN Anywhere
```

## Bloquear número da porta já liberada

```
sudo ufw delete ${numero_sequencia_porta}
```
