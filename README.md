```
const botconfig = require("./botconfig.json");
const tokenfile = require("./token.json");
const quotebank = require("./quotebank.json");
const quoteImageUrl = require("./quoteImageUrl.json");
const exbank = require("./exbank.json");
const Discord = require("discord.js");
const bot = new Discord.Client({disableEveryone: true});

bot.on("ready", async () => {
  console.log(`${bot.user.username} is ready to train and fight!`);
  bot.user.setActivity("Training!");

});

//Sends a hello message to the sever//
/* bot.on("ready", () => {
  var channel = bot.channels.get('525705828905386005');
  channel.send("***Let's Train and Fight!***");
});*/
//bot commands
bot.on("message", async message => {
  if(message.author.bot) return;
  if(message.channel.type === "dm") return;

  let prefix = botconfig.prefix;
  //let messageArray = message.content.split(" ");
  //let cmd = messageArray[0];
  //let args = messageArray.slice(1);

  const args = message.content.slice(prefix.length).trim().split(/ +/g);
  const cmd = args.shift().toLowerCase();



// wb!help - List of commands
  if(cmd === `${prefix}help`){

    let hicon = message.guild.displayAvatarURL;
    let helpembed = new Discord.RichEmbed()
    .setDescription("Here is a helpful list of commands")
    .setColor("#9106a0")
    .setThumbnail(hicon)
    .addField("wb!help", "Brings up this list")
    .addField("wb!botinfo", "Gives you information about WarriorBot")
    .addField("wb!serverinfo", "Gives you info about the server")
    .addField("wb!quote", "Gives you a random quote from WarriorMale")
    .addField("wb!workout", "Gives you 3 random exercises to do")
    .addField("wb!pic", "Gives you a random picture");

    return message.channel.send(helpembed)

}

// wb!serverinfo - Displays info about the server
  if(cmd === `${prefix}serverinfo`){

    let sicon = message.guild.displayAvatarURL;
    let serverembed = new Discord.RichEmbed()
    .setDescription("Server Information")
    .setColor("#9106a0")
    .setThumbnail(sicon)
    .addField("Server Name", message.guild.name)
    .addField("Created On", message.guild.createdAt)
    .addField("You Joined", message.guild.joinedAt)
    .addField("Total Members", message.guild.memberCount);

    return message.channel.send(serverembed)
}

// wb!botinfo - Displays info about WarriorBot
  if(cmd === `${prefix}botinfo`){

    let bicon = bot.user.displayAvatarURL;
    let botembed = new Discord.RichEmbed()
    .setDescription("Bot Information")
    .setColor("#9106a0")
    .setThumbnail(bicon)
    .addField("Bot Name", bot.user.username)
    .addField("Created On", bot.user.createdAt);

    return message.channel.send(botembed);

}
//wb!pic - Gives you a random picture
  if(cmd === `${prefix}pic`){

  let number = 11;

  let imageNumber = Math.floor((Math.random() * (number - 1 + 1)) + 1);

  message.channel.send( {files: ["./images/" + imageNumber + ".jpg"]} )

}


//wb!quote - Gives you a random WarriorMale quote
 if(cmd === `${prefix}quote`){

    const quote = (quotebank.quote);
    const quoteImage = (quoteImageUrl.picture);

    let result1 = Math.floor((Math.random() * quote.length));
    let result5 = Math.floor((Math.random() * quoteImage.length));

    const quoteEmbed = new Discord.RichEmbed()
      .setAuthor(message.author.tag)
      .setColor("#9106a0")
      .addField("A quote for you from WarriorMale", quote[result1])
      .setImage(quoteImage[result5]);

  message.channel.send(quoteEmbed)

}

/*
//wb!workout - Gives you a some random exercises to do
 if(cmd === `${prefix}workout`){

      let woArg = ["arms", "legs", "chest", "back"]


        switch (woArg) {

          case "arms":

            let number1 = Math.floor(Math.random() * 20) + 10;
            let number2 = Math.floor(Math.random() * 20) + 10;
            let number3 = Math.floor(Math.random() * 20) + 10;
            let setNumber = Math.floor(Math.random() * 5) + 1;

            let exercise1 = (exbank.arms1);
            let exercise2 = (exbank.arms2);
            let exercise3 = (exbank.arms3);

            let result2 = Math.floor((Math.random() * exercise1.length));
            let result3 = Math.floor((Math.random() * exercise2.length));
            let result4 = Math.floor((Math.random() * exercise3.length));

            const workoutEmbed = new Discord.RichEmbed()
              .setAuthor(message.author.tag)
              .setColor("#9106a0")
              .setDescription("***Ready, Set, Train!***")
              .addField("Exercise 1", number1 + " " + exercise1[result2])
              .addField("Exercise 2", number2 + " " + exercise2[result3])
              .addField("Exercise 3", number3 + " " + exercise3[result4])
              .addField("How many sets?", "***" + setNumber + " SETS!***");

              message.channel.send(workoutEmbed)

              break;

          case "legs":

            let number1A = Math.floor(Math.random() * 20) + 10;
            let number2A = Math.floor(Math.random() * 20) + 10;
            let number3A = Math.floor(Math.random() * 20) + 10;
            let setNumberA = Math.floor(Math.random() * 5) + 1;

            let exercise1A = (exbank.legs1);
            let exercise2A = (exbank.legs2);
            let exercise3A = (exbank.legs3);

            let result2A = Math.floor((Math.random() * exercise1A.length));
            let result3A = Math.floor((Math.random() * exercise2A.length));
            let result4A = Math.floor((Math.random() * exercise3A.length));

            const workoutEmbedA = new Discord.RichEmbed()
              .setAuthor(message.author.tag)
              .setColor("#9106a0")
              .setDescription("***Ready, Set, Train!***")
              .addField("Exercise 1", number1A + " " + exercise1A[result2A])
              .addField("Exercise 2", number2A + " " + exercise2A[result3A])
              .addField("Exercise 3", number3A + " " + exercise3A[result4A])
              .addField("How many sets?", "***" + setNumberA + " SETS!***");

              message.channel.send(workoutEmbedA)

              break;

          case "chest":

            let number1B = Math.floor(Math.random() * 20) + 10;
            let number2B = Math.floor(Math.random() * 20) + 10;
            let number3B = Math.floor(Math.random() * 20) + 10;
            let setNumberB = Math.floor(Math.random() * 5) + 1;

            let exercise1B = (exbank.chest1);
            let exercise2B = (exbank.chest2);
            let exercise3B = (exbank.chest3);

            let result2B = Math.floor((Math.random() * exercise1B.length));
            let result3B = Math.floor((Math.random() * exercise2B.length));
            let result4B = Math.floor((Math.random() * exercise3B.length));

            const workoutEmbedB = new Discord.RichEmbed()
              .setAuthor(message.author.tag)
              .setColor("#9106a0")
              .setDescription("***Ready, Set, Train!***")
              .addField("Exercise 1", number1B + " " + exercise1B[result2B])
              .addField("Exercise 2", number2B + " " + exercise2B[result3B])
              .addField("Exercise 3", number3B + " " + exercise3B[result4B])
              .addField("How many sets?", "***" + setNumberB + " SETS!***");

              message.channel.send(workoutEmbedB)

              break;

          case "back":

            let number1C = Math.floor(Math.random() * 20) + 10;
            let number2C = Math.floor(Math.random() * 20) + 10;
            let number3C = Math.floor(Math.random() * 20) + 10;
            let setNumberC = Math.floor(Math.random() * 5) + 1;

            let exercise1C = (exbank.back1);
            let exercise2C = (exbank.back2);
            let exercise3C = (exbank.back3);

            let result2C = Math.floor((Math.random() * exercise1C.length));
            let result3C = Math.floor((Math.random() * exercise2C.length));
            let result4C = Math.floor((Math.random() * exercise3C.length));

            const workoutEmbedC = new Discord.RichEmbed()
              .setAuthor(message.author.tag)
              .setColor("#9106a0")
              .setDescription("***Ready, Set, Train!***")
              .addField("Exercise 1", number1C + " " + exercise1C[result2C])
              .addField("Exercise 2", number2C + " " + exercise2C[result3C])
              .addField("Exercise 3", number3C + " " + exercise3C[result4C])
              .addField("How many sets?", "***" + setNumberC + " SETS!***");

              message.channel.send(workoutEmbedC)

              break;

          default:
              let number1D = Math.floor(Math.random() * 20) + 10;
              let number2D = Math.floor(Math.random() * 20) + 10;
              let number3D = Math.floor(Math.random() * 20) + 10;
              let setNumberD = Math.floor(Math.random() * 5) + 1;

              let exercise1D = (exbank.exercise1);
              let exercise2D = (exbank.exercise2);
              let exercise3D = (exbank.exercise3);

              let result2D = Math.floor((Math.random() * exercise1D.length));
              let result3D = Math.floor((Math.random() * exercise2D.length));
              let result4D = Math.floor((Math.random() * exercise3D.length));

              const workoutEmbedD = new Discord.RichEmbed()
                .setAuthor(message.author.tag)
                .setColor("#9106a0")
                .setDescription("***Ready, Set, Train!***")
                .addField("Exercise 1", number1D + " " + exercise1D[result2D])
                .addField("Exercise 2", number2D + " " + exercise2D[result3D])
                .addField("Exercise 3", number3D + " " + exercise3D[result4D])
                .addField("How many sets?", "***" + setNumberD + " SETS!***");

            message.channel.send(workoutEmbedD)

          }

}
*/






});

bot.login(tokenfile.token);

```
