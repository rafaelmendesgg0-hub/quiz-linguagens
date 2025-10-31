<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
     <title>Qual é a Sua Linguagem? - Quiz de Perfil</title>
    <style>
        /* CSS para Estilizar o Quiz */
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f9;
            color: #333;
            display: flex;
            justify-content: center;
            align-items: flex-start;
            padding: 20px;
        }

        .container {
            background-color: #fff;
            padding: 30px;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            max-width: 700px;
            width: 100%;
        }

        h1, h2 {
            text-align: center;
            color: #007bff;
        }

        .pergunta-container {
            margin-bottom: 20px;
            padding: 15px;
            border: 1px solid #ddd;
            border-radius: 6px;
            background-color: #fafafa;
        }

        .pergunta-container label {
            display: block;
            padding: 10px;
            margin: 5px 0;
            cursor: pointer;
            border: 1px solid #ccc;
            border-radius: 4px;
            transition: background-color 0.3s;
        }

        .pergunta-container label:hover {
            background-color: #e9ecef;
        }

        .pergunta-container input[type="radio"] {
            margin-right: 10px;
        }

        #botao-resultado {
            display: block;
            width: 100%;
            padding: 15px;
            background-color: #28a745;
            color: white;
            border: none;
            border-radius: 6px;
            font-size: 1.1em;
            cursor: pointer;
            transition: background-color 0.3s;
            margin-top: 20px;
        }

        #botao-resultado:hover {
            background-color: #218838;
        }

        /* Seção do Resultado (escondida inicialmente) */
        #resultado-secao {
            display: none; /* ESSENCIAL: Escondido inicialmente */
            margin-top: 30px;
            padding: 20px;
            border: 2px solid #007bff;
            border-radius: 8px;
            background-color: #e9f5ff;
        }

        #resultado-titulo {
            font-size: 1.5em;
            color: #007bff;
            margin-bottom: 10px;
        }
        
        #resultado-descricao {
            white-space: pre-wrap; /* Mantém a formatação com quebras de linha */
        }
    </style>
</head>
<body>

    <div class="container">
        <h1>Qual é a Sua Linguagem?</h1>
        <p style="text-align: center;">Responda às 15 perguntas para descobrir qual Linguagem de Programação ou Marcação mais combina com o seu perfil.</p>

        <form id="quiz-form">
            </form>

        <button id="botao-resultado">Ver Meu Perfil</button>

        <div id="resultado-secao">
            <h2 id="resultado-titulo"></h2>
            <p id="resultado-descricao"></p>
        </div>
    </div>

    <script>
        // ----------------------------------------------------
        // Lógica do Quiz em JavaScript
        // ----------------------------------------------------

        // 1. Definição das Perguntas e Respostas
        // Cada resposta tem um valor (A, B, C, D) que corresponde a um perfil.
        const perguntas = [
            {
                pergunta: "1. Qual é a sua prioridade em um projeto de software?",
                opcoes: [
                    { texto: "Ter a solução mais clara, legível e concisa (rápida de desenvolver).", valor: 'A' },
                    { texto: "Criar uma experiência dinâmica, visual e responsiva para o usuário.", valor: 'B' },
                    { texto: "Garantir que a aplicação seja robusta e escalável para milhões de usuários.", valor: 'C' },
                    { texto: "Tornar a apresentação visualmente agradável e bem estruturada.", valor: 'D' }
                ]
            },
            {
                pergunta: "2. Qual tipo de problema você mais gosta de resolver?",
                opcoes: [
                    { texto: "Análise de dados, Machine Learning ou automação de tarefas.", valor: 'A' },
                    { texto: "Interatividade, animações e o comportamento no navegador.", valor: 'B' },
                    { texto: "Arquitetura de sistemas complexos e gestão de concorrência.", valor: 'C' },
                    { texto: "Organização do layout, hierarquia de conteúdo e design responsivo.", valor: 'D' }
                ]
            },
            {
                pergunta: "3. Você prefere ser visto como...",
                opcoes: [
                    { texto: "O cientista que descobre padrões e otimiza a lógica.", valor: 'A' },
                    { texto: "O mágico que faz as coisas se moverem e interagir.", valor: 'B' },
                    { texto: "O arquiteto que constrói a fundação sólida e confiável.", valor: 'C' },
                    { texto: "O designer que define a aparência e a usabilidade.", valor: 'D' }
                ]
            },
            {
                pergunta: "4. O que mais te incomoda em um código?",
                opcoes: [
                    { texto: "Código lento e desnecessariamente verboso.", valor: 'A' },
                    { texto: "Incompatibilidade entre navegadores e bugs em tempo de execução.", valor: 'B' },
                    { texto: "Falta de estrutura e tipagem que leva a erros em projetos grandes.", valor: 'C' },
                    { texto: "Um elemento desalinhado por 1 pixel ou falta de padronização visual.", valor: 'D' }
                ]
            },
            {
                pergunta: "5. Como você aborda a criação de uma nova página web?",
                opcoes: [
                    { texto: "Focando em como o servidor processa os dados antes de enviar a página.", valor: 'A' },
                    { texto: "Pensando em como a página irá interagir e mudar após o carregamento.", valor: 'B' },
                    { texto: "Definindo a arquitetura do servidor e os módulos de backend primeiro.", valor: 'C' },
                    { texto: "Começando pela estrutura (<div>, <p>, <h1>) e o estilo visual.", valor: 'D' }
                ]
            },
             {
                pergunta: "6. Você valoriza mais...",
                opcoes: [
                    { texto: "A velocidade de desenvolvimento (prototipagem rápida).", valor: 'A' },
                    { texto: "A versatilidade para rodar em quase todo ambiente (frontend e backend).", valor: 'B' },
                    { texto: "A segurança do tipo (Strong Typing) e a estabilidade a longo prazo.", valor: 'C' },
                    { texto: "A facilidade de aprendizado e a renderização imediata de resultados.", valor: 'D' }
                ]
            },
             {
                pergunta: "7. Se o código fosse um livro, você estaria mais preocupado com:",
                opcoes: [
                    { texto: "A clareza da linguagem e a organização concisa dos capítulos.", valor: 'A' },
                    { texto: "As notas de rodapé dinâmicas e as ilustrações interativas.", valor: 'B' },
                    { texto: "A solidez da encadernação e a durabilidade do papel (longa vida útil).", valor: 'C' },
                    { texto: "O design da capa, a tipografia e o índice bem formatado.", valor: 'D' }
                ]
            },
             {
                pergunta: "8. Qual a sua visão sobre tipagem de dados?",
                opcoes: [
                    { texto: "Tipagem dinâmica é ótima para rapidez e flexibilidade (menos burocracia).", valor: 'A' },
                    { texto: "Tipagem dinâmica, mas com a opção de tipagem estática (ex: TypeScript) é o ideal.", valor: 'B' },
                    { texto: "Tipagem estática é essencial para grandes projetos e controle de erros.", valor: 'C' },
                    { texto: "Tipagem de dados não é uma preocupação central para o meu foco.", valor: 'D' }
                ]
            },
             {
                pergunta: "9. Você prefere escrever código que:",
                opcoes: [
                    { texto: "Faz muito em poucas linhas, com sintaxe quase natural.", valor: 'A' },
                    { texto: "É assíncrono e baseado em eventos/promessas.", valor: 'B' },
                    { texto: "É verboso, mas explicito e seguro em cada etapa.", valor: 'C' },
                    { texto: "Define o que cada coisa é e onde deve estar.", valor: 'D' }
                ]
            },
            {
                pergunta: "10. Você se considera mais...",
                opcoes: [
                    { texto: "Um resolvedor de problemas lógicos e matemáticos.", valor: 'A' },
                    { texto: "Um construtor de experiências interativas.", valor: 'B' },
                    { texto: "Um engenheiro de software focado em performance e manutenção.", valor: 'C' },
                    { texto: "Um arquiteto de conteúdo e design visual.", valor: 'D' }
                ]
            },
            {
                pergunta: "11. Como você lida com mudanças constantes nas tecnologias?",
                opcoes: [
                    { texto: "Adoto mudanças se elas tornarem o código mais limpo ou rápido.", valor: 'A' },
                    { texto: "Estou acostumado, a evolução é a parte mais divertida!", valor: 'B' },
                    { texto: "Prefiro tecnologias com comunidades maduras e menos quebras de compatibilidade.", valor: 'C' },
                    { texto: "Mantenho a simplicidade, as mudanças afetam o meu trabalho minimamente.", valor: 'D' }
                ]
            },
            {
                pergunta: "12. Qual é a sua reação a um erro no código?",
                opcoes: [
                    { texto: "Reviso a lógica e a clareza para encontrar a solução elegante.", valor: 'A' },
                    { texto: "Uso o console do navegador e procuro o ponto exato da falha assíncrona.", valor: 'B' },
                    { texto: "Busco o stack trace para entender a exceção na máquina virtual.", valor: 'C' },
                    { texto: "Confiro o inspetor de elementos para ver se a estrutura ou estilo estão quebrados.", valor: 'D' }
                ]
            },
            {
                pergunta: "13. Qual é o seu ambiente de desenvolvimento favorito?",
                opcoes: [
                    { texto: "Um ambiente de console ou notebook (Jupyter) para testes rápidos.", valor: 'A' },
                    { texto: "O próprio navegador e o ecossistema Node.js.", valor: 'B' },
                    { texto: "Uma IDE completa e pesada, com depuração avançada.", valor: 'C' },
                    { texto: "Um editor leve com extensões de visualização ao vivo.", valor: 'D' }
                ]
            },
            {
                pergunta: "14. Você prioriza a estética ou a função do código?",
                opcoes: [
                    { texto: "Função, mas com altíssima prioridade na legibilidade e clareza.", valor: 'A' },
                    { texto: "Ambos, pois o código deve entregar uma função visual e interativa.", valor: 'B' },
                    { texto: "Função, a estética deve ser padronizada para manter a performance.", valor: 'C' },
                    { texto: "Estética, a beleza da estrutura e do layout é o mais importante.", valor: 'D' }
                ]
            },
            {
                pergunta: "15. O que te faz sentir que o trabalho está COMPLETO?",
                opcoes: [
                    { texto: "Todos os testes de unidade passaram e a performance é ótima.", valor: 'A' },
                    { texto: "O usuário final está interagindo com a interface de forma fluida e sem bugs.", valor: 'B' },
                    { texto: "O código compilou sem warnings e o projeto segue a arquitetura definida.", valor: 'C' },
                    { texto: "O design está perfeito em todos os dispositivos e o conteúdo está bem hierarquizado.", valor: 'D' }
                ]
            }
        ];

        // 2. Definição dos Perfis (Resultado Final)
        const perfis = {
            'A': {
                titulo: "Seu Perfil: Python (O Cientista de Dados)",
                descricao: "Você valoriza a clareza, a simplicidade e o poder de fazer muito com pouco código. Seu foco está na *lógica de negócios, na **análise de dados* e na *automação* (Backend). Você busca soluções elegantes e de rápida implementação. O ecossistema de Data Science, Machine Learning e Web moderna (Flask/Django) é o seu habitat natural.",
                cor: '#3572A5'
            },
            'B': {
                titulo: "Seu Perfil: JavaScript (O Construtor de Experiências)",
                descricao: "Você é dinâmico, adaptável e focado na *interação. O ambiente do navegador é o seu playground, mas sua versatilidade permite que você atue em qualquer lugar (Full Stack). Você abraça a mudança e adora construir interfaces ricas e complexas usando frameworks como **React, Vue ou Angular*. O futuro é assíncrono e você está na vanguarda.",
                cor: '#F7DF1E'
            },
            'C': {
                titulo: "Seu Perfil: Java / C# (O Arquiteto de Sistemas)",
                descricao: "Sua prioridade é a *estabilidade, a **escalabilidade* e a *segurança*. Você se sente mais confortável em sistemas grandes, robustos e corporativos, onde a performance e a manutenção a longo prazo são cruciais. A tipagem estática e a arquitetura bem definida são essenciais para você. Você é o engenheiro que constrói pontes que duram décadas.",
                cor: '#007396'
            },
            'D': {
                titulo: "Seu Perfil: HTML & CSS (O Designer de Conteúdo)",
                descricao: "Você é um *arquiteto visual* e um mestre da organização. Sua paixão está em estruturar o conteúdo e garantir que ele seja apresentado de forma perfeita e acessível em qualquer tela. Você valoriza a usabilidade, a estética e o design responsivo. Sua contribuição é garantir que a fundação e a apresentação de toda a aplicação sejam impecáveis.",
                cor: '#E34F26'
            }
        };

        // Variável de pontuação
        let pontuacoes = { 'A': 0, 'B': 0, 'C': 0, 'D': 0 };

        // 3. Função para Renderizar as Perguntas
        function renderizarPerguntas() {
            const quizForm = document.getElementById('quiz-form');
            perguntas.forEach((p, index) => {
                const container = document.createElement('div');
                container.classList.add('pergunta-container');
                
                const perguntaTexto = document.createElement('p');
                perguntaTexto.textContent = p.pergunta;
                container.appendChild(perguntaTexto);

                p.opcoes.forEach(opcao => {
                    const label = document.createElement('label');
                    const input = document.createElement('input');
                    
                    input.type = 'radio';
                    input.name = `pergunta${index}`;
                    input.value = opcao.valor; // O valor que será somado (A, B, C, D)
                    
                    label.appendChild(input);
                    label.appendChild(document.createTextNode(opcao.texto));
                    container.appendChild(label);
                });

                quizForm.appendChild(container);
            });
        }

        // 4. Função Principal para Calcular e Mostrar o Resultado
        function calcularResultado() {
            // 1. Zera a pontuação para garantir novo cálculo e prepara o objeto
            pontuacoes = { 'A': 0, 'B': 0, 'C': 0, 'D': 0 };

            // 2. Coleta e Soma os Pontos
            const respostas = new FormData(document.getElementById('quiz-form'));
            let todasRespondidas = true;
            
            for (let i = 0; i < perguntas.length; i++) {
                const nomeCampo = `pergunta${i}`;
                const respostaValor = respostas.get(nomeCampo); // Pega o valor (P, J, C ou H)

                if (respostaValor) {
                    pontuacoes[respostaValor]++;
                } else {
                    todasRespondidas = false;
                }
            }

            if (!todasRespondidas) {
                alert('Por favor, responda a todas as 15 perguntas antes de ver o resultado.');
                return;
            }

            // 3. Determina o Perfil Vencedor
            let perfilVencedor = '';
            let pontuacaoMaxima = -1;

            for (const perfil in pontuacoes) {
                if (pontuacoes[perfil] > pontuacaoMaxima) {
                    pontuacaoMaxima = pontuacoes[perfil];
                    perfilVencedor = perfil;
                }
                // Simplificação: o primeiro perfil em caso de empate vence
            }

            // 4. Obtém os dados do resultado (título, descrição, cores)
            const resultado = perfis[perfilVencedor];
            const resultadoSecao = document.getElementById('resultado-secao');
            const resultadoTitulo = document.getElementById('resultado-titulo');
            const resultadoDescricao = document.getElementById('resultado-descricao');

            // 5. ATUALIZA O CONTEÚDO
            resultadoTitulo.textContent = resultado.titulo;
            resultadoDescricao.textContent = resultado.descricao;
            
            // 6. APLICA AS CORES DINÂMICAS! (O trecho que você precisa)
            resultadoSecao.style.backgroundColor = resultado.cor; // Cor de fundo
            resultadoSecao.style.borderColor = resultado.cor;       // Cor da borda
            // A cor do texto será a corTexto se definida, senão, branco por padrão ('#ffffff')
            resultadoSecao.style.color = resultado.corTexto || '#ffffff'; 
            
            // Garante que o título dentro do bloco também use a cor do texto principal
            resultadoTitulo.style.color = resultado.corTexto || '#ffffff'; 

            // 7. MOSTRA O BLOCO DE RESULTADO
            resultadoSecao.style.display = 'block';

            // 8. Rolagem suave para o resultado
            resultadoSecao.scrollIntoView({ behavior: 'smooth' });
        }

        // 5. Inicia o Quiz e Adiciona o Evento ao Botão
        document.addEventListener('DOMContentLoaded', () => {
            renderizarPerguntas();
            document.getElementById('botao-resultado').addEventListener('click', calcularResultado);
        });

    </script>
    <script src="script.js"></script>


</body>
</html>
