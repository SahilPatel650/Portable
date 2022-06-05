For youtubedl:
IN YoutubeDL.py
for i, entry in enumerate(entries, 1):
            self.to_screen('[download] Downloading video %s of %s' % (i, n_entries))

ADD:
if os.path.basename(os.getcwd()) != "NA":
                Process=subprocess.Popen('progressBar %s %s' % (str(i-1),str(n_entries),), shell=True)
                Process=subprocess.Popen('echo "%s" > posfile; echo "%s" >> posfile' % (str(i-1),str(n_entries),), shell=True)
            
        
IN common.py
def report_progress(self, s):

at the top

ADD:
if os.path.basename(os.getcwd()) == "NA":
            Process=Popen('curr="%s"; final="%s"; progressBar $curr $final' % (str(s.get('downloaded_bytes')),str(s.get('total_bytes')),), shell=True)
        else:
            Process=Popen('pos=`awk "NR==1 {print; exit}" posfile`; total=`awk "NR==2 {print; exit}" posfile`; curr="%s"; final="%s"; progressBar `echo "frac=($curr/$final+$pos)*10000; scale=0; frac/1" | bc -l` $((total*10000))' % (str(s.get('downloaded_bytes')),str(s.get('total_bytes')),), shell=True)
