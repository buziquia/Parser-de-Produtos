CRUD REST API - Projeto Laravel
Este projeto é uma REST API desenvolvida em Laravel, que inclui operações de CRUD (Create, Read, Update, Delete) e funcionalidades adicionais para importar e atualizar dados a partir do Open Food Facts.

Funcionalidades da API
GET /: Retorna detalhes da API, como status de conexão com o banco de dados, horário da última execução do cron, tempo online e uso de memória.
GET /products: Lista todos os produtos na base de dados com paginação.
GET /products/
: Retorna os detalhes de um produto específico com base em seu código.
PUT /products/
: Atualiza as informações de um produto específico.
DELETE /products/
: Altera o status de um produto para "trash" (exclusão lógica).
Estrutura de Banco de Dados
A tabela products foi criada com os seguintes campos:

id: Identificador único.
code: Código único do produto.
name: Nome do produto.
description: Descrição do produto.
price: Preço do produto.
status: Status do produto (active ou trash).
timestamps: Marcas de tempo de criação e atualização.
Configuração do Docker
Este projeto utiliza o Docker com Laravel Sail para facilitar a execução e o desenvolvimento local.

Comandos para Iniciar o Projeto
Subir o ambiente com Docker e Sail:

bash
Copiar código
./vendor/bin/sail up -d
Instalar as dependências do Composer:

bash
Copiar código
./vendor/bin/sail composer install
Rodar as migrações para criar as tabelas:

bash
Copiar código
./vendor/bin/sail artisan migrate
Comandos para Importar Dados do Open Food Facts
Para atualizar a base de dados com dados do Open Food Facts, um comando de importação pode ser criado. Aqui está um exemplo de como rodar um script de importação:

bash
Copiar código
./vendor/bin/sail artisan import:products
Este comando deve ser configurado para buscar os dados do site e fazer a importação para a base de dados, limitando a importação a 100 produtos por arquivo.

Testes Unitários
O projeto inclui testes unitários para garantir o funcionamento correto da API.

Comandos para Rodar os Testes
bash
Copiar código
./vendor/bin/sail artisan test
Os testes incluem verificações para todos os endpoints principais da API, como listar produtos, buscar por código, atualizar e excluir.

Estrutura de Código
app/Models/Product.php: Modelo do produto.
app/Http/Controllers/ProductController.php: Controlador contendo as operações CRUD.
routes/api.php: Definições de rotas da API.
database/migrations/xxxx_xx_xx_create_products_table.php: Migração para a tabela products.
tests/Feature/ProductApiTest.php: Testes unitários para a API.
Comandos Úteis
Limpar cache de configuração:

bash
Copiar código
./vendor/bin/sail artisan config:cache
Gerar uma nova chave de aplicação:

bash
Copiar código
./vendor/bin/sail artisan key:generate
Executar o Cron de Atualização
Adicione um agendamento ao Laravel para rodar o comando de importação uma vez ao dia:

php
Copiar código
// No arquivo App\Console\Kernel.php
protected function schedule(Schedule $schedule)
{
    $schedule->command('import:products')->dailyAt('03:00');
}
Conclusão
Este projeto fornece uma API completa com um CRUD de produtos, integração com dados externos e execução em ambiente Docker. Sinta-se à vontade para explorar, modificar e expandir as funcionalidades conforme necessário.
