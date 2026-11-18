# SSH Auth Action

Composite action to setup SSH authentication. It creates SSH key ~/.ssh/id_rsa which you can pass to SSH commands.

## Usage Example

```yml
name: Deploy

on:
  push:
    branches: [master]

jobs:
  deploy:
    name: Deploy
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v6

      - name: Create SSH key
        uses: SerhiiChoAction/ssh-auth@v1
        with:
          host-user: ${{ secrets.HOST_USER }}
          host-ip: ${{ secrets.HOST_IP }}
          host-key: ${{ secrets.HOST_PRIVATE_SSH_KEY }}

      - name: Restart destination server
        run: |
           ssh ${{ secrets.HOST_USER }}@${{ secrets.HOST_IP }} "cd ~/project && ./cmd/restart"
```
