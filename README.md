      sound on
      mode 6
      
      rem Define Characters
      vdu 23,240,124,144,159,249,185,175,40,238
      vdu 23,241,255,255,255,255,255,255,255,255
      vdu 23,242,248,136,62,123,125,127,127,62
      vdu 23,243,60,94,143,223,255,255,126,60
      
      rem Build Characters
      Sold$=chr$(17)+chr$(5)+chr$(240)
      Block$=chr$(17)+chr$(2)+chr$(241)
      Bomb$=chr$(17)+chr$(9)+chr$(242)
      Clear$=chr$(17)+chr$(4)+chr$(243)
      
      
      proc_Preset
      
      rem Opening
      
      proc_title
      wait 20
      proc_menu
      
      mode 6
      
      off
      
      
      
      
      print tab(Player.x%,Player.y%); Sold$
      
      
      
      
      
      proc_Borders
      proc_Block
      proc_Clear
      
      repeat
        
        proc_displayStats
        proc_ShowBombs
        
        proc_Movement
        
        
        proc_getMoreBombs
        proc_removeBombs
        
        if Player.y% = 0 or Player.y% = 20 or Player.x% = 0 or Player.x% = 24 then
          Player.Lives% = Player.Lives%-1
        endif
        
        if paused2% = true then
          if Player.x% = Clear.x% and Player.y% = Clear.y% then
            Score2%=Score2%-50
            CD% = CD%-1
            Mines%=Mines%+1
            proc_Clear
            paused2% = false
          endif
        endif
        
        if Player.x% = Block.x% and Player.y% = Block.y% then
          Player.Score%=Player.Score%+10
          Score2%=Score2%+10
          proc_Block
        else
          print tab(Block.x%,Block.y%); Block$
        endif
        
        for n% = 1 to BOMBS%
          if Player.x% = Bombx%(n%) and Player.y% = Bomby%(n%) and found% = true then
            Player.Lives% = Player.Lives% - 1
          endif
        next
        
      until Player.Lives%=0
      rem Display
      cls
      colour 7
      print tab(13,12);"You scored ";Player.Score%
      on
      
      sound off
      proc_Rainbow
      proc_Finish
      
      end
      
      rem END OF MAIN PROGRAM
      rem USER DEFINED PROC
      rem -------------------------------------------------------------------------------------------------------------------------------------------------
      
      
      
      def proc_Rainbow
      sound 2, 0,0,25
      sound 3, 0,0,25
      sound 2, -15, 68, 15
      sound 3, -15, 80, 15
      sound 2, 0,0,65
      sound 3, 0,0,65
      sound 2, -15, 68, 10
      sound 3, -15, 80, 10
      sound 2, 0,0,300
      sound 3, 0,0,300
      
      
      sound 1, -15, 100, 5
      sound 1, 0, 0, 5
      sound 1, -15, 100, 5
      sound 1, -15, 108, 5
      sound 1, -15, 116, 5
      sound 1, -15, 100, 5
      sound 1, -15, 116, 5
      sound 1, -15, 120, 5
      
      sound 1, -15, 128, 5
      sound 1, 0, 0, 5
      sound 1, -15, 128, 5
      sound 1, -15, 120, 5
      sound 1, -15, 116, 10
      
      sound 1, 0, 0, 10
      sound 1, -15, 108, 5
      sound 1, 0, 0, 5
      sound 1, -15, 108, 5
      sound 1, 0, 0, 5
      sound 1, -15, 108, 10
      sound 1, 0, 0, 5
      
      sound 1, -15, 108, 2
      sound 1, 0, 0, 2
      sound 1, -15, 108, 2
      sound 1, 0, 0, 2
      sound 1, -15, 116, 5
      sound 1, -15, 108, 5
      sound 1, -15, 100, 5
      sound 1, -15, 80, 12
      sound 1, 0, 0, 3
      
      sound 1, -15, 80, 2
      sound 1, 0, 0, 2
      sound 1, -15, 100, 5
      sound 1, 0, 0, 5
      sound 1, -15, 100, 5
      sound 1, -15, 108, 5
      sound 1, -15, 116, 5
      sound 1, -15, 100, 5
      sound 1, -15, 116, 5
      sound 1, -15, 120, 5
      
      sound 1, -15, 128, 5
      sound 1, 0, 0, 5
      sound 1, -15, 128, 5
      sound 1, -15, 120, 5
      sound 1, -15, 116, 17
      sound 1, 0, 0, 3
      
      sound 1, -15, 108, 5
      sound 1, 0, 0, 5
      sound 1, -15, 108, 5
      sound 1, 0, 0, 5
      sound 1, -15, 116, 12.5
      sound 1, -15, 108, 5
      sound 1, -15, 100, 5
      sound 1, 0, 0, 5
      sound 1, -15, 100, 5
      sound 1, 0, 0, 5
      sound 1, -15, 100, 10
      sound 1, 0, 0, 5
      
      cls
      endproc
      
      
      def proc_title
      rem title screen
      cls
      *font Courier new, 50bu
      colour 5
      printtab(2,1)"Space Blocks"
      *font Courier new, 20b
      colour 3
      printtab(14)"Harry Li"
      print " "
      colour 2
      *font Arial, 20b
      printtab(23)"Computing GCSE Game"
      wait 50
      *font, Courier new, 14
      print ''
      endproc
      
      
      def proc_menu
      rem displays and runs a menu
      local g$
      colour 1
      *font Verdana, 16b
      printtab(23)"Press 'i' for instructions"
      printtab(23) "Press 'q' to toggle music"
      printtab(13)"Press any other key to start the game!"
      g$ = get$
      
      if g$ = "i" or g$ = "I" then
        proc_instructions
      endif
      
      if g$ = "q" or g$ = "Q" then
        proc_music
      endif
      endproc
      
      def proc_music
      cls
      *font Courier new, 50bu
      colour 6
      printtab(5,0)"Music!"
      *font Arial, 15b
      local g$
      printtab(5)"Press the following numbers to change your choice of music:"
      print " "
      colour 3
      *font Verdana, 15
      printtab(2)"1",; "Little Fugue - JS Bach"
      printtab(2)"2",; "koto"
      printtab(2)"3",; "Pokémon Battle"
      printtab(2)"4",; "Berceuse - Fauré"
      printtab(2)"5",; "40th Symphony - Mozart"
      printtab(2)"6",; "Sugar Plum Fairies - Tchaikovsky"
      printtab(2)"7",; "Sonata 3 - Mozart"
      printtab(2)"8",; "Funky"
      printtab(2)"9",; "Music off"
      print " "
      *font Arial, 15b
      colour 6
      printtab(5)"The music may take a while to load. "
      printtab(5)"When you are happy with your selection"
      printtab(5)"Press 'm' to return to the menu"
      *font Arial, 12
      colour 2
      printtab(5)"During the game, press 'p' to change your music choice"
      
      repeat
        g$ = get$
        case g$ of
            
          when "1"
            procLoadAndPlayMIDITune( @dir$ + "resources\music\Little Fugue.MID" )
          when "2"
            procLoadAndPlayMIDITune( @dir$ + "resources\music\koto.MID" )
          when "3"
            procLoadAndPlayMIDITune( @dir$ + "resources\music\pokemontrain.MID" )
          when "4"
            procLoadAndPlayMIDITune( @dir$ + "resources\music\Fauré.MID" )
          when "5"
            procLoadAndPlayMIDITune( @dir$ + "resources\music\Mozart.MID" )
          when "6"
            procLoadAndPlayMIDITune( @dir$ + "resources\music\Sugar.MID" )
          when "7"
            procLoadAndPlayMIDITune( @dir$ + "resources\music\Sonata.MID" )
          when "8"
            procLoadAndPlayMIDITune( @dir$ + "resources\music\1gyp1.MID" )
          when "9"
            sound off
            
        endcase
      until g$ = "m"
      run
      endproc
      
      def proc_Music
      rem cls
      local g$
      colour 3
      printtab(25,11)"1:Little Fugue"
      printtab(25,12)"2:koto"
      printtab(25,13)"3:PokémonBattle"
      printtab(25,14)"4:Berceuse"
      printtab(25,15)"5:40th Symphony"
      printtab(25,16)"6:Fairies"
      printtab(25,17)"7:Sonata 3"
      printtab(25,18)"8:Funky"
      printtab(25,19)"9:Music off"
      colour 6
      rem printtab(26,19)"The music may take a while to load. "
      rem printtab(26,20)"When you are happy with your selection"
      rem printtab(26,21)"Press 'm' to return to the game"
      
      repeat
        g$ = get$
        case g$ of
            
          when "1"
            procLoadAndPlayMIDITune( @dir$ + "resources\music\Little Fugue.MID" )
          when "2"
            procLoadAndPlayMIDITune( @dir$ + "resources\music\koto.MID" )
          when "3"
            procLoadAndPlayMIDITune( @dir$ + "resources\music\pokemontrain.MID" )
          when "4"
            procLoadAndPlayMIDITune( @dir$ + "resources\music\Fauré.MID" )
          when "5"
            procLoadAndPlayMIDITune( @dir$ + "resources\music\Mozart.MID" )
          when "6"
            procLoadAndPlayMIDITune( @dir$ + "resources\music\Sugar.MID" )
          when "7"
            procLoadAndPlayMIDITune( @dir$ + "resources\music\Sonata.MID" )
          when "8"
            procLoadAndPlayMIDITune( @dir$ + "resources\music\1gyp1.MID" )
          when "9"
            sound off
            
        endcase
      until g$ = "p"
      endproc
      
      
      
      def proc_instructions
      local g
      cls
      colour 1
      *font Courier new, 50bu
      colour 6
      printtab(2,1)"Space Blocks"
      *font Courier new, 14b
      colour 1
      print
      printtab(15)"Press arrow keys to move"
      printtab(5)"Press <space> to use a mine to clear the screen"
      printtab(16)"Press <s> for suicide"
      print
      colour 2:printtab(2)Sold$,;:colour1:print"You";
      colour 2:printtab(40)Clear$,;:colour1:print"Mine"
      colour 7:printtab(2)Bomb$,;:colour1:print"Bomb";
      colour 9:printtab(2)Block$,;:colour1:print"Block";
      print '
      printtab(14)"Collect Blocks to gain points"
      printtab(14)"Bombs will spawn everytime you move"
      printtab(14)"Avoid Bombs or you will lose a life!"
      printtab(14)"AVOID BORDERS - YOU WILL LOSE ALL LIVES!"
      printtab(14)"You only have 3 lives!"
      print " "
      colour 2
      *font Verdana, 8
      print "Press m to go back to the menu"
      
      g$ = get$
      if g$ = "m"  run
      wait 20
      endproc
      
      def proc_Borders
      for S%=1 to 20
        print tab(0,S%); Bomb$
      next
      
      for s%=0 to 24
        print tab(s%,0); Bomb$
      next
      
      for Z%=1 to 20
        print tab(24,Z%); Bomb$
      next
      
      for z%=0 to 24
        print tab(z%,20); Bomb$
      next
      endproc
      
      def proc_Finish
      colour 7
      *font Verdana, 20
      input "Would you like to play again? (y/n) : " answer$
      if answer$ = "y" or answer$ = "Y" or answer$ = "yes" or answer$ = "Yes" or answer$ = "YES" or answer$ = "yES" or answer$ = "yeS" or answer$ = "YeS" or answer$ = "YEs" then
        run
      endif
      
      if answer$ = "n" or answer$ = "N" or answer$ = "no" or answer$ = "No" or answer$ = "NO" or answer$ = "nO" then
        printtab(13,12); "Thank you for playing!"
        proc_Tune
      endif
      endproc
      
      def proc_Clear
      
      Clear.x% = rnd(22)+1
      Clear.y% = rnd(18)+1
      
      for Interval% = 50 to 10000 step 50
        for Negative% = 1 to 100 step 1
          if Score2%=Interval% and CD%=101-Negative% then
            print tab(Clear.x%,Clear.y%); Clear$
            if notpaused2% then
              paused2% = true
            endif
          endif
        next
      next
      endproc
      
      def procLoadAndPlayMIDITune( file$ )
      local F%
      sound off
      sys "PlaySound", 0, 0, 0
      F% = openin( file$ )
      oscli "PLAY """+file$+""""
      endproc
      
      def proc_Tune
      repeat
        
        rem Bar 1
        sound 1, -15, 108, 5
        sound 1, -15, 88, 5
        sound 1, -15, 108, 5
        sound 1, -15, 136, 5
        sound 1, 0, 0, 5
        sound 1, -15, 128, 5
        sound 1, 0, 0, 5
        sound 1, -15, 124, 5
        
        rem Bar 2
        sound 1, -15, 116, 5
        sound 1, -15, 104, 20
        sound 1, 0, 0, 15
        
        rem Bar 3
        sound 1, -15, 104, 5
        sound 1, -15, 88, 5
        sound 1, -15, 104, 5
        sound 1, -15, 124, 5
        sound 1, 0, 0, 5
        sound 1, -15, 116, 5
        sound 1, 0, 0, 5
        sound 1, -15, 104, 5
        
        rem Bar 4
        sound 1, -15, 108, 5
        sound 1, -15, 124, 20
        sound 1, 0, 0, 15
        
        rem Bar 5
        sound 1, -15, 108, 5
        sound 1, -15, 88, 5
        sound 1, -15, 108, 5
        sound 1, -15, 136, 5
        sound 1, 0, 0, 5
        sound 1, -15, 128, 5
        sound 1, 0, 0, 5
        sound 1, -15, 124, 5
        
        rem Bar 6
        sound 1, -15, 116, 5
        sound 1, -15, 104, 20
        sound 1, 0, 0, 15
        
        rem Bar 7
        sound 1, -15, 104, 5
        sound 1, -15, 88, 5
        sound 1, -15, 104, 5
        sound 1, -15, 124, 5
        sound 1, 0, 0, 5
        sound 1, -15, 116, 5
        sound 1, 0, 0, 5
        sound 1, -15, 104, 5
        
        rem Bar 8
        sound 1, -15, 108, 20
        sound 1, 0, 0, 20
        
        rem Bar 9
        sound 1, -15, 124, 15
        sound 1, 0, 0, 5
        sound 1, -15, 136, 15
        sound 1, 0, 0, 5
        
        rem Bar 10
        sound 1, -15, 128, 5
        sound 1, -15, 136, 5
        sound 1, -15, 128, 5
        sound 1, -15, 124, 5
        sound 1, -15, 116, 15
        sound 1, 0, 0, 5
        
        rem Bar 11
        sound 1, -15, 104, 15
        sound 1, 0, 0, 5
        sound 1, -15, 116, 15
        sound 1, 0, 0, 5
        
        rem Bar 12
        sound 1, -15, 124, 5
        sound 1, -15, 128, 5
        sound 1, -15, 124, 5
        sound 1, -15, 116, 5
        sound 1, -15, 108, 15
        sound 1, 0, 0, 5
        
        rem Bar 13
        sound 1, -15, 124, 15
        sound 1, 0, 0, 5
        sound 1, -15, 136, 15
        sound 1, 0, 0, 5
        
        rem Bar 14
        sound 1, -15, 128, 5
        sound 1, -15, 124, 5
        sound 1, -15, 128, 5
        sound 1, -15, 136, 5
        sound 1, -15, 144, 15
        sound 1, 0, 0, 5
        
        rem Bar 15
        sound 1, -15, 136, 10
        sound 1, -15, 128, 5
        sound 1, -15, 124, 5
        sound 1, -15, 128, 15
        sound 1, 0, 0, 5
        
        rem Bar 16
        sound 1, -15, 124, 5
        sound 1, -15, 128, 5
        sound 1, -15, 124, 5
        sound 1, -15, 116, 5
        sound 1, -15, 108, 15
        sound 1, 0, 0, 5
        
      until false
      endproc
      
      defproc_displayStats
      rem display the players stats on the right hand side of the screen
      colour 1
      printtab(27,6)"Mines : ";:colour3:printstr$(Mines%)"  "
      printtab(27,7)"Score  : ";:colour5:printstr$(Player.Score%)"  "
      printtab(27,8)"Lives  : ";:colour6:printstr$(Player.Lives%)"  "
      endproc
      
      def proc_Movement
      rem Movement
      
      local g%
      DELAY% = 4
      time = 1
      g% = inkey(DELAY%)
      wait (DELAY% - time)
      
      case g% of
          
        when 136:
          rem if Player.x%>0 then
          Player.x%=Player.x%-1
          if fn_canMove(Player{}, 3) then
            print tab(Player.x%,Player.y%); Sold$
            print tab(Player.x%+1,Player.y%);" "
            rem proc_checkBomb
          endif
          
          
        when 137:
          if fn_canMove(Player{}, 1) then
            Player.x%=Player.x%+1
            print tab(Player.x%,Player.y%); Sold$
            print tab(Player.x%-1,Player.y%);" "
            rem proc_checkBomb
          endif
          
        when 138:
          if fn_canMove(Player{}, 2) then
            Player.y%=Player.y%+1
            print tab(Player.x%,Player.y%); Sold$
            print tab(Player.x%,Player.y%-1);" "
            rem proc_checkBomb
          endif
          
        when 139:
          if fn_canMove(Player{}, 0) then
            Player.y%=Player.y%-1
            print tab(Player.x%,Player.y%); Sold$
            print tab(Player.x%,Player.y%+1);" "
            rem proc_checkBomb
          endif
          
        when 32:
          if Mines%>0 then
            Mines%=Mines%-1
            proc_removeBombs
            proc_Borders
            print tab(Player.x%,Player.y%); Sold$
          endif
          
        when 112,80
          if notpaused% then
            paused% = true
            colour 3
            printtab(29,2)"Paused"
            proc_Music
            printtab(29,2)"      "
            printtab(25,11)"               "
            printtab(25,12)"               "
            printtab(25,13)"               "
            printtab(25,14)"               "
            printtab(25,15)"               "
            printtab(25,16)"               "
            printtab(25,17)"               "
            printtab(25,18)"               "
            printtab(25,19)"               "
            paused% = false
          endif
          
        when 115: Player.Lives%=Player.Lives%-1
          
      endcase
      endproc
      
      def proc_ShowBombs
      local n%
      local found%
      
      for n% = 1 to BombPointer%
        print tab(Bombx%(n%),Bomby%(n%)); Bomb$
        found% = true
      next
      endproc
      
      defproc_getMoreBombs
      rem procedure decides whether or not to add a new bomb to the field
      if BombPointer% < BOMBS% then
        if rnd(BOMB_CHANCE%) = 1 then
          BombPointer% += 1
        endif
      endif
      endproc
      
      def proc_removeBombs
      local n%
      local found%
      while n%< BombPointer% and notfound%
        for n% = 1 to BombPointer%
          if notbombGone%(n%) then
            printtab(Bombx%(n%),Bomby%(n%)); " "
            found% = true
            bombGone%(n%) = true
          endif
        next
      endwhile
      endproc
      
      def proc_Preset
      rem Preset Numbers
      local n%
      dim Player{x%,y%,Score%,Lives%,Sold$}
      Player.x% = 4
      Player.y% = 4
      Player.Lives% = 3
      Player.Score% = 0
      
      BOMBS% = 580
      dim Bombx%(BOMBS%)
      dim Bomby%(BOMBS%)
      dim bombGone%(BOMBS%)
      
      dim Block{x%,y%,r%,Name$}
      
      dim Clear{x%,y%}
      
      BombPointer% = 0
      Score2%=0
      Mines% = 1
      CD% = 100
      BOMB_CHANCE% = 4
      paused%=false
      paused2%=false
      
      for n% = 1 to BOMBS%
        Bombx%(n%) = rnd(24) : rem store a rnd position for the bomb
        Bomby%(n%) = rnd(20) : rem store a rnd position for the bomb
        bombGone%(n%) = false
      next
      endproc
      
      
      def proc_Block
      local n%
      local found%
      found% = false
      rem Random Block Colour
      
      Block.x% = rnd(22)+1
      Block.y% = rnd(18)+1
      Block.r% = rnd(14)
      Block$=chr$(17)+chr$(Block.r%+1)+chr$(241)
      
      repeat
        for n% = 1 to BombPointer%
          if Block.x% = Bombx%(n%) and Block.y% = Bomby%(n%) then
            found% = false
          endif
        next
        Block.x% = rnd(22)+1
        Block.y% = rnd(18)+1
      until Block.x% <> Bombx%(n%) or Block.y% <> Bomby%(n%)
      found% = true
      
      print tab(Block.x%,Block.y%); Block$
      
      endproc
      
      def fn_canMove(Player{}, direction% )
      rem can the player move in the direction indicated
      rem 0 up, 1 right 2 down, 3 left
      rem Find location in which Player wants to move to
      local xp%, yp%
      local Result%
      case direction% of
          
          
        when 0
          yp% = -1
          row%=get(Player.x%,Player.y%+yp%)
          if row% = 242 then
            Player.Lives% = Player.Lives% - 1
          endif
          
          
        when 1
          xp% = 1
          row%=get(Player.x%+xp%,Player.y%)
          if row% = 242 then
            Player.Lives% = Player.Lives% - 1
          endif
          
        when 2
          yp% = 1
          row%=get(Player.x%,Player.y%+yp%)
          if row% = 242 then
            Player.Lives% = Player.Lives% - 1
          endif
          
        when 3
          xp% = -1
          row%=get(Player.x%,Player.y%)
          if row% = 242 then
            Player.Lives% = Player.Lives% - 1
          endif
          
      endcase
      
      rem check boundary conditions (FRAME OF LEVEL)
      if Player.y%+yp% <=0 then
        Result%=false
      endif
      if Player.y%+yp% > 20 then
        Result%=false
      endif
      if Player.x%+xp% <=1 then
        Result% =false
      endif
      if Player.x%+xp% > 24 then
        Result%=false
      endif
      =true
