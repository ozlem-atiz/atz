# atz
I created the box files with the QT-Box-Editor application on windows. I confirmed and edited the correctness of the characters one by one with this tool.

(in CMD)


Step 1: Creating for box files
tesseract [langname].[fontname].[expN].[file-extension] [langname].[fontname].[expN] batch.nochop makebox
EX: tesseract own.arial.exp0.jpg own.arial.exp0 batch.nochop makebox
{*Note:After making box files we have to change or modify wrongly identified characters in box files.}


Step 2: Create .tr file (Compounding image file and box file)
tesseract [langname].[fontname].[expN].[file-extension] [langname].[fontname].[expN] box.train
EX: tesseract own.arial.exp0.jpg own.arial.exp0 box.train


step 3: Extract the charset from the box files (Output for this command is unicharset file)
unicharset_extractor [langname].[fontname].[expN].box 
EX:unicharset_extractor  own.arial.exp0.box


step 4: Create a font_properties file based on our needs.
echo "[fontname] [italic (0 or 1)] [bold (0 or 1)] [monospace (0 or 1)] [serif (0 or 1)] [fraktur (0 or 1)]" > font_properties 
EX: echo "arial 0 0 1 0 0" > font_properties


Step 5: Training the data.
mftraining -F font_properties -U unicharset -O [langname].unicharset [langname].[fontname].[expN].tr
Ex: mftraining -F font_properties -U unicharset -O own.unicharset own.arial.exp0.tr


Step 6:cntraining [langname].[fontname].[expN].tr
EX: cntraining own.arial.exp0.tr
{*Note:After step 5 and step 6 four files were created.(shapetable,inttemp,pffmtable,normproto) }


Step 7: Rename four files (shapetable,inttemp,pffmtable,normproto) into ([langname].shapetable,[langname].inttemp,[langname].pffmtable,[langname].normproto)
rename filename1 filename2
EX:
    rename shapetable own.shapetable
    rename inttemp own.inttemp
    rename pffmtable own.pffmtable
    rename normproto own.normproto
    
    
Step 8: Create .traineddata file
combine_tessdata [langname].
EX:combine_tessdata own.

