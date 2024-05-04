# Rock_Paper_Scissors.io

<!DOCTYPE html>
<html>
    <head>
        <title>10-Rock Paper Scissors</title>
        <style>
            body{
                background-color: black;
                color: white;
            }
            .User_choose{
                display: flex;
                justify-content: center;
                align-items: center;
                width: 100%;
                height: 100%;
            }
            .game_name{
                text-align: center;
                font-size: 50px;
            }
            img{
                max-width: 130px; /* Ensures the image doesn't exceed its container */
                height: 120px; /* Allows the image to maintain its aspect ratio */
                display: block; /* Ensures proper rendering */
                margin: 0 auto; /* Centers the image horizontally */
                border-color: rgb(248, 141, 0);

            }
            button{
                cursor: pointer;
            }
            
            button:hover{
                transform: translateY(-2px);
            }

            .Choose_Rock, .Choose_Paper, .Choose_Scissors{
                background-color: transparent;
                border: 5px solid #fafafa;
                border-radius: 55px;
                margin-right: 10px;
            }

            .User_choose{
                margin-bottom: 20px;
            }
            .anounce_section{
                display: flex;
                flex-direction: column;
                justify-content: center;
                align-items: center;
                width: 100%;
                height: 100%; 
            }
            .js-result, .js-moved, .js-score{
                font-size: 20px;
                font-weight: bold;
                margin-top: 0px;
                margin-bottom: 15px;  
            }
            .js-moved{
                display: flex;
                align-items: center;
            }
            ._move{
                width: 60px;
                height: 60px;
            }
            .button_reset{
                display: flex;
                align-items: center;
                justify-content: center;
            }
            .choose_reset{
                padding: 10px 20px;
                border-radius: 50px;
                background-color: rgb(181, 206, 228);
                border: none;
                color: #070707;
                font-size: 24px;
                font-weight: bold;
            }
        </style>
    </head>
    <body>
        <div>
            <div>
                <p class = "game_name">Rock Paper Scissors</p>
            </div>
            <div class ="User_choose">
                <button class = "Choose_Rock" onclick="
                    play('Rock');
                "><img src="Image/Rock1.png">
                </button>

                <button class = "Choose_Paper" onclick="
                    play('Paper');
                "><img src="Image/Paper1.png">
                </button>

                <button class = "Choose_Scissors" onclick="
                    play('Scissors');
                "><img src="Image/Scissors1.png">
                </button>
            </div>
            <div class = "anounce_section">
                <p class="js-result"> Result </p>
                <p class="js-moved"></p>
                <p class="js-score"> Win: 0, Lose: 0, Tie: 0</p>
            </div>
            <div class = button_reset>
                <button class = "choose_reset" onclick="
                        reset_game();
                    ">Reset
                </button>
            </div>
        </div>

        <script>
            let score = JSON.parse(localStorage.getItem
            ('score')) || {
                    win: 0,
                    lose: 0,
                    tie: 0
                };
            

            function reset_game(){
                score.win = 0;
                score.lose = 0;
                score.tie = 0;
                localStorage.removeItem('score');

                document.querySelector('.js-result')
                    .innerText = 'Result';
                document.querySelector('.js-moved')
                    .innerText = '';
                document.querySelector('.js-score')
                    .innerHTML = `Win: ${score.win}, Lose: ${score.lose}, Tie: ${score.tie}`;
            } 
            function play(user){
                const cmpter = computerMove();

                document.querySelector('.js-score')
                    .innerHTML = `Win: ${score.win}, Lose: ${score.lose}, Tie: ${score.tie}`;
                console.log(cmpter);
                
                localStorage.setItem('score', JSON.stringify(score));

                let result = '';
                
                if(user === 'Paper'){
                    if(cmpter === 'Rock'){
                        result = 'You win!';
                    }
                    else if(cmpter === 'Paper'){
                        result = 'Tie';
                    }
                    else if(cmpter === 'Scissors'){
                        result = 'You lose';
                    }
                }
                
                if(user === 'Scissors'){
                    if(cmpter === 'Rock'){
                        result = 'You lose';
                    }
                    else if(cmpter === 'Paper'){
                        result = 'You win!';
                    }
                    else if(cmpter === 'Scissors'){
                        result = 'Tie';
                    }
                }
                
                if(user === 'Rock'){
                    if(cmpter === 'Rock'){
                        result = 'Tie';
                    }
                    else if(cmpter === 'Paper'){
                        result = 'You lose';
                    }
                    else if(cmpter === 'Scissors'){
                        result = 'You win!';
                    }
                }
                
                if(result === 'You win!'){
                    score.win++;
                }
                else if(result === 'You lose'){
                    score.lose++;
                }
                else if(result === 'Tie'){
                    score.tie++;
                }
                
                localStorage.setItem('score', JSON.stringify(score));

                document.querySelector('.js-result')
                    .innerHTML = result;

                document.querySelector('.js-moved')
                    .innerHTML = `You picked <img class = "_move" src="Image/${user}.png"> || computer picked <img class = "_move" src="Image/${cmpter}.png">`;
                    //`You picked ${user} || Computer picked ${cmpter}`;

                document.querySelector('.js-score')
                    .innerHTML = `Win: ${score.win}, Lose: ${score.lose}, Tie: ${score.tie}`;


            }
            
            function computerMove(){
                let cmpter = '';

                const randnum = Math.random();

                if(randnum >= 0 && randnum < 1/3){
                    cmpter = 'Rock';
                }
                else if(randnum >= 1/3 && randnum < 2/3){
                    cmpter = 'Paper';
                }
                else if(randnum >= 2/3 && randnum < 1){
                    cmpter = 'Scissors';
                }
                
                return cmpter;
            }
        </script>
    </body>
</html>
