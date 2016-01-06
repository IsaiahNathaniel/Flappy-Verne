var game = new Phaser.Game(400, 490, Phaser.AUTO, 'gameDiv');

// main state of game
var mainState = {
    
    // loads game assets
    preload: function() {
        // background color
        game.stage.backgroundColor = '#71c5cf';
        // load bird asset
        game.stage.image('bird', 'assets/bird.png');    
    },
    
    // set up game, display sprites, etc
    create: function() {
        // set physics
        game.physics.startSystem(Phaser.Physics.ARCADE);
        // display bird
        this.bird = this.game.add.sprite(100, 245, 'bird');
        // add gravity to bird
        game.physics.arcade.enable(this.bird)
        this.bird.body.gravity.y = 1000;
        // jump function
        var spaceKey = this.game.input.keyboard.addKey(Phaser.Keyboard.SPACEBAR);
        spaceKey.onDown.add(this.jump, this);
    },
    
    // called 60 times per second contains games logic
    update: function() {
        // checks for world leaving
        if (this.bird.inWorld == false)
            this.restartGame();
    },
    jump: function() {
        //adds vertical velocity
        this.bird.body.velocity.y -350;
    },
    restartGame: function() {
        // Restarts gamae
        game.state.start('main')
    },
};

game.state.add('main', mainState);
game.state.start('main');

