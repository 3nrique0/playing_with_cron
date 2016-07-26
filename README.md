# Monitor QSE activity using CRON, QSUB and TOP #


## Welcome message ##

I sometimes need to monitor the resource consumption some tasks on a QSE.
Therefore I needed to create some automated way of doing it.


The path and username will be deliverately named $USER and $path
For the noobs, the variables in UPPER-CASE belong to the system, wheres lower-case are given by the user.

 Please be welcome to use/copy and request details about the usage. Since this is a personal repository for a specific QSE system, things may variate, with pleasure I'll help make things more... generic.

 Enjoy !!
 3nrique0


### How it works ###

In order to use a crontab you need to have a simple executable script, monitor_clusterjob.sh. This script contains the qsub command.

The qsub command contains the parameters in the executable script qsub_parameters.sh. This script contains another executable which contains the job you want to send. In this case we want to send a top command located in my_script.sh

So the order of scripts calling scripts goes as following:

monitor_clusterjob.sh --> qsub qsub_parameters.sh --> my_script.sh

my_script.sh can contain anything you want to execute in the cluster
qsub_parameters.sh contains the parameters to submit it
monitor_clusterjob.sh is the single thing which will be repeatedly submitted.

### Manual ###
Once you launched a long process on a QSE, with the right options!!, you should prepare :
1. my_script.sh with the top command you want to use. I'd advise to use the name of the process to grep the line you want.

2. chmod +x my_script.sh

3. Check the script qse_launcher.sh: qsub qse_launcher.sh

4. Check the crontable you need, some examples are in crontable_examples : 
	online help:
	http://askubuntu.com/questions/2368/how-do-i-set-up-a-cron-job
	http://stackoverflow.com/questions/5398014/using-crontab-to-execute-script-every-minute-and-another-every-24-hours
	
5. Launch cron:
Add the crontable with the command 'crontable -e' (no quotes!)
Write the table you require. e.g. every 15 min:
/15 * * * * /homedir/$USER/path/.monitor_clusterjob.sh



######
Description
######

Files:

my_script.sh : Script containing the top command or your own pipeline to be used in the QSE

qse_launcher.sh : Script containing the options for QSE. Please take note of the -o  amd -e options allowing to manage output and error files to a specific file. This files are in append mode. So you'll need to empty them manually when finished.

top_commnads : Propositions of top commands to filter the top results to only have the results you want to have. The easiest way would be to filter by name.


