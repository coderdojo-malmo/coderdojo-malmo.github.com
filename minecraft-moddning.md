---
title: Minecraft Moddning
layout: page
---
# CoderDojo: Minecraft Moddning

### Nivå 0: CoderDojo – installera Eclipse och dekompilera minecraft

Att börja moddna minecraft måste du först ha en ren minecraft (en minecraft utan andra modder).

Då installera du kanske:

* jdk (java developer kit)
* ire (java runtime environment)
* eclipse (en app att programmera i java)
* mcp (mine craft coder pack)

Detta kan du hitta på internet, usb stickan eller PirateBoxen.

Efter du har anstellerat allt, kan du dekompilera koden.

**Windows**

1. tryck på kör i meny
2. söka till %appdata%
3. kopiera mappar  minecraft/bin och minecraft/resources till mappen mcp726a/jars
4. dubbel tryck på mcp726a/decompile.sh

**Mac**

1. navigera till ~/Library/Application Support/minecraft
2. kopiera mappar bin och resources till mappen: mcp726a/jars
3. kör terminal.app
4. cd i till mcp726a
5. kör bash decompile.sh

Om du har  problemmer och måste installera något annat då måste du kör mcp726a/cleanup.bat innan du kan försöka dekompilera igen.

### Nivå 1: Slime – skapa en ny block med den egna recept

När du kör Eclipse första gången måste du indentifera i vilken verkplats ditt projekt ligger. Navigera till mcp723/eclipse och tryck på OK.

Minecraft källkoden ligger under Client/src/net.minecraft.src. Hitta det på vänster sid av Eclipse i Package Explorer fönstret. Här finns nästan alla filer minecraft kör ifrån. Oppna Block.java.

Block.java är en objektklass. Det är föräldern till alla andra blocker som minecraft har.

Hitta linjen:

	    public static final Block stone = (new BlockStone(1, 1)).setHardness(1.5F).setResistance(10.0F).setStepSound(soundStoneFootstep).setBlockName("stone");

Det är en deklaration av en typ av block: en sten. Varje block har ditt eget nummer. Sten har numret 1. Vilken block har numret 86?

Eftersom Mojang fortfarande utvecklar Minecraft kan du se att nya blocker har högra nummer än gamla. När du skapa ditt eget block måste du välja ett nummer ingen annan block använda.

**Din först block**

Skapa en ny klass. Jag kaller min BlockExampel att följer konventionen men du kan kalla det vad som helst. Kopiera koden i till ny klass.

	package net.minecraft.src;
	import java.util.Random;

	/* Koden användar namnet BlockExampel. Byta det till namnet som du har valt. */

	public class BlockExampel extends Block
	{
		public BlockExample(int i, int j)
		{
			super(i, j, Material.rock);
		}

		public int idDropped(int i, Random random)
		{
			return 0;
		}
	}

Kanske sog du att en linje är inte kod utan på svenska. När man programmera det är en bra idé att kommentera vad du skriver. Då om en annan person (eller en äldre du) läsa koden kan de bättre förstå vad du menade. Kommenter på java, börja med /* och sluta med */. Om du göra inte det din kod kommer att inte fungera.

I filen block.java måste du nu deklara din egen block.

Under sista deklaration tillägger linjen:

	public static final Block exampel = (new BlockExample(92, 1)).setHardness(1.5F).setResistance(10F).setStepSound(soundStoneFootstep);

Byta namnet 'exampel' och numret '92'. Kommentera vad du har gjört.

Nu är vi klar att kör Minecraft. Spara allt och tryck på 'Run'.

Börja en ny kreativ värld med bedrageren aktiverat.

Kör kommand:

/give Player 92 64

Istället än 'Player' använda ditt spelarenamn (skriv 'P' och tryck tab) och istället än 92 använda block numret.

Om alla fungera bra ha du din ny block.

Försöka att göra din block hårdare. Försöka att göra din block unbreakable (tip: vilken block är redo unbreakable).

**Block recepten**

Nu kan vi börja ge ditt block en recept.

Öppna filen CraftingManager.java i Eclipse.

Navigera till linjen:

	this.addRecipe(new ItemStack(Item.sign, 3), new Object[] {"###", "###", " X ", '#', Block.planks, 'X', Item.stick});

Här finns där alla informationer vi behöver att skapa en skylt i Minecraft. Tänker nu hur man göra det i en crafting box.

I först ruta behöver man tre plankar. I andra är det samma. Men i sista behöver man bara en pinne i mellan plats. Titta på koden och tänker på hur det fungera (tip: # betyder plank och X stick).

Observera att skylt och pinne är inte en block utan en item. Det är en viktig skillnad. Vad andra kunde vara en item i Minecraft?

Under sista recepten tillägger linjen:

	addRecipe(new ItemStack(Block.exampel, 1), new Object[] {"# #", " # ", "# #", '#', Block.dirt});

Byta namnet 'exampel. Kommentera vad du har gjört.

Vad är recepten här. Skriva den på en lapp.

Spara koden och kör Minecraft. Se om du kan spara din block utan kommander.

Byta recepten till någonting med två blocker. Försöka en recept med itemer.

### Nivå 2: Blaze – skapa en ny vapen med den egen textur
### Nivå 3: Creeper – skapa en kustom npc med den egen ljud
### Nivå 4: Steve – hjälp en annan person till nivå creeper
### Nivå 5: Ender Dragon – gör din eget mod och låda det upp till minecraft forumer
