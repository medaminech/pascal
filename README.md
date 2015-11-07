program ex4s3;
uses wincrt;
var

f,ft:text;
ligne:string;
i:integer;

procedure affichage(var ft:text);
begin
reset(f);
while (not(eof(ft))) do
begin
readln(ft,ligne);
writeln(ligne);
end;
end;

procedure creation(var ft:text);
begin
assign(ft,'document.txt');
rewrite(ft);
end;

procedure remplissage(var ft:text);
begin
reset(ft);
writeln('Tapez le ''.'' pour sortir.');
repeat
writeln('Tapez une ligne');
readln(ligne);
append(ft);
writeln(ft,ligne);
until (ligne[length(ligne)]='.');
end;

procedure correction(var f,ft:text);
begin
assign(ft,'correction.txt');
rewrite(ft);
assign(f,'document.txt');
reset(f);
while(not(eof(f))) do
begin
readln(f,ligne);
while(ligne[1]=' ' ) do
delete(ligne,1,1);
i:=1;
while(i<=length(ligne)) do
begin
if(ligne[i]=' ' ) and (ligne[i+1]=' ' ) then
delete(ligne,1,1)
else
inc(i);
end;
if ligne[length(ligne)]<>'.' then
ligne:=ligne+ '.' ;
append(ft);
writeln(ft,ligne);
end;
close(ft);
close(f);
end;
begin
creation(f);
remplissage(f);
correction(f,ft);
writeln('Le fichier d''origine : ');affichage(f);
writeln('Le fichier correction :');affichage(ft);
end.
