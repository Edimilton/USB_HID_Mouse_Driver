# Driver de Mouse USB Personalizado para Linux
Este é um driver de mouse USB personalizado para o kernel Linux. Projetado para melhorar a experiência de navegação para pessoas com deficiência (PCD). Quando ativado através de um botão lateral, este driver permite um controle preciso e simplificado do cursor, facilitando a navegação em toda a tela com pequenos movimentos. Siga as instruções abaixo para compilar, carregar e remover o módulo do kernel.

## Pré-requisitos

Certifique-se de ter os seguintes itens instalados no seu sistema antes de prosseguir:

- [Linux Kernel](https://www.kernel.org/)
- [Make](https://www.gnu.org/software/make/)
- Permissões de administrador (ou use `sudo` conforme necessário)

## Passo 1: Indentificando o modulo padrão


### Consulte o arquivo de log do kernel para coletar informações sobre o módulo padrão do mouse que está sendo usado:
```
dmesg | grep -i mouse
```

### Liste todos os módulos carregados no kernel atual e filtre os resultados para encontrar o módulo relacionado ao mouse:
```
lsmod | grep -i mouse
```

### Verifique os módulos relacionados ao dispositivo de entrada:
```
lsmod | grep input
```

### Verifique o mapeamento do dispositivo de entrada:
```
ls /dev/input/
```

### Para determinar qual módulo de kernel está associado a esses dispositivos de entrada, você pode usar o seguinte comando:
```
cat /proc/bus/input/devices
```

## Passo 2: Carregando o Módulo Personalizado

### Você precisa remover o módulo padrão que controla o mouse. Substitua `nome_do_modulo_padrao` pelo nome do módulo que você identificou no passo 1:
```
sudo rmmod nome_do_modulo_padrao
```

### Use o comando `make` no diretorio do arquivo usbmousepwd.c para gerar o arquivo `.ko`:
```
make
```

### Para carregar o módulo personalizado, use o seguinte comando:
```
sudo insmod usbmousepwd.ko
```

## Removendo o Módulo Personalizado
### Caso deseje remover o módulo personalizado, utilize o seguinte comando:
```
sudo rmmod usbmousepwd
```




Se você tiver algum problema ou dúvida, verifique as mensagens de erro e consulte a documentação do kernel para solucionar problemas adicionais.
