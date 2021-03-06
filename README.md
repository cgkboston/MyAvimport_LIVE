# MyAvimport_LIVE
This is an implementation of various Netsmart webservices including the Cache 2017 required security header.
Please see the VERY IMPORTANT note at the end of this readme.txt file.

This code is currently monolithic meaning we recompile for Sandbox, UAT and live.  You have the option to combine all of the Connected Services into 
one App.config/myAvimport.csproj file.  To do this, update the Designer to reduce the size of the light coral text box that says something like 
myAvatar ... myAvimport ... LIVE.  This will reveal the environment radio buttons after you compile.  You'd have figured this out eventually.

There are other changes to make, e.g. the environment setting within the application MyAvimport.cs file, remove the hardcoded SystemCode and also 
increase the number of case statements in the various code switches throughout the application (refer to {
UserManagement,ClientAdmission,CrossEpFinancialElig}.cs.  You'll also need to add using statements for all three Avatars and check your App.config
and your MyAvatar.csproj to make sure Visual Studio handles all of this correctly for you.  Oh and one other change, the application title bar will 
need to be made variable.

I found it easier to continue on my predecesor's (The eponymous Chris Banwarth) path and keep the code monolithic, but I'm not saying it can't be 
made pluralistic, ..., have at it at your own peril.

Environment Microsoft Visual Studio community edition, coded in C#.

Should you decide to keep the code monolithic here's a useful powershell script
gci *.*|foreach-object {
echo $_.FullName
get-content $_.FullName | select-string 'LIVE','UAT','Sandbox','SBOX'
}

you can leave the radio buttons but the above will reveal other places to change for your UAT or Sandbox (SBOX) environments.
or leave the code monolithic and just update the case "SBOX":, the using, the systemcode and the _Sandbox on the connected services to your 
environment (e.g. live or UAT).  Also change the windows title in the designer file

A couple of programming notes: 
1. we set this up to import Larry's Thom clients from moon island.  Since these clients are in the 2 year old range we set the employer to null and
the smoking status to unknown, :).  The streetline 2 is set to space when not available to allow the Netsmart web service to work.  Some of the other
fields are also either set to null or space.  Finally we store the mbhp id in the freetxt_20_1 field (SSDemographicsFreeText201).  This is a recent 
addition to Larry's input files.  Don't ask anything more about Larry, according to my colleague Larry is Thom and that's all you need to know.
______________________________________________________
** VERY IMPORTANT: ** If you change nothing else before you compile, update to your AVATAR in the wsdl, configuration{91}.svcinfo 
and App.config files, (all part of the Netsmart connected web services).
Faiulure to do so will surely fail because you will not have access to my Avatar.
TO DO THIS: ** before compiling the application **
cd $installFolder
dir
PS C:\Users\...\source\repos\MyAvimport\myAvimport_LIVE> Get-ChildItem -Recurse '.\Connected Services\*\*.*'| ForEach-Object {
>> echo "Process $_"
>> ((Get-Content -path $_ -Raw) -replace 'YOURAVATAR','$YOURAVATAR') |Set-Content -Path $_.FullName
>> }

** EQUALLY IMPORTANT: ** ALSO set $YOURAVATAR in the App.Config prior to compiling the application in Visual Studio 2019.
Also consider changing the name of your .sln file to for example MyAvimport_{SBOX, UAT, LIVE}

Where $YOURAVATAR corresponds to Your Avatar hosted avatar server (Sandbox, UAT or LIVE).
______________________________________________________
Feel free to contact Chris ckennedy@aspirehealthalliance.org (or preferably Pat: priley@ssmh.org) for help or questions or refer to apcp, ntst or 
github (cgkboston)

Chris Kennedy for Pat Riley
cgkboston@gmail.com
339.201.0243
September 2020.
with a huge shout out to the eponymous original author (Chris Banwarth) and webmaster @aprettycoolprogram.com without whose advice and consent none of this would be possible.
_________________________________
PostScript Note to Matt 3/5/2021: 

Here are the powerShell commands I discussed earlier.  These commands will help you to set the variable YourAvatarHost to your actual Avatar Host
Just Change $YourAvatarHost with the host name for your Avatar Host.

\CKENNEDY\Desktop\AVIMPORT_LIVE_Release> gci *.* -Recurse|Select-String YourAvatarHost -List|Measure-Object -Line

Lines Words Characters Property
----- ----- ---------- --------
   14
PS C:\Users\CKENNEDY\Desktop\AVIMPORT_LIVE_Release> gci *.* -Recurse -Exclude *.json*,*1.0,*1.3,.vs |foreach {
>> (Get-Content $_ | foreach {$_ -replace "YourAvatarHost","$YourAvatarHost"}) | Set-Content $_
>> }                                                                                                                                          
PS C:\Users\CKENNEDY\Desktop\AVIMPORT_LIVE_Release>                                                                                           
This project should compile after the change above and allow you to connect to Intersystems Cache 2017 with the 
rquired Security Header Class supplied by ntst for Cache 2017.

Finally the full list of Netsmart Web Services which can be implemented with the Security Header are in the file
Netsmart Web Services.docx in this file.  The word doc contains links to the netsmart web site for each of the 
web services.  Enjoy.

Chris Kennedy
3/5/2021
