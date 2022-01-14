import os
import glob

def get_ids_from_path_pattern(path_pattern):
    ids = sorted([os.path.basename(os.path.splitext(val)[0])
                  for val in (glob.glob(path_pattern))])
    return ids

IDs = get_ids_from_path_pattern('models/*')

rule all:
    input:
        expand(f'sim_detailed/{{IDs}}/done.log', IDs=IDs)
    shell:
        """
        echo "Gathering {input} ... "
        """

rule smetana_global:
    input:
        f'models/{{IDs}}'
    output:
        f'sim/{{IDs}}/done.log'
    message:
    	"""
    	This rule will look for communities of GEMs in the models subdir and simulate them 100 times using the SMETANA global algorithm
    	Assumes GEMs were carved using the cobra flag
    	"""
    shell:
        """
        # Activate conda environment
        echo -e "Activating conda environment ... "
        set +u;source activate carve;set -u;

        # This is just to make sure that output folder exists
        mkdir -p $(dirname {output})

        # Move to input folder with GEMs subdir
        cd {input}

        # Run SMETANA on loop 100 times
        for i in {{1..100}}; do echo "Running simulation $i out of 100 ... "; smetana --flavor ucsd -o ../../$(dirname {output})/sim_${{i}}.tsv -v -g models/*.xml; done

        # Create dummy file and return to original dir
        cd ../..
        touch {output}
        """

rule smetana_detailed_gut:
    input:
        f'models/{{IDs}}'
    output:
        f'sim_detailed/{{IDs}}/done.log'
    message:
    	"""
    	This rule will look for communities of GEMs in the models subdir and simulate them using the SMETANA detailed algorithm
    	Assumes GEMs were carved using the cobra flag
    	"""
    shell:
        """
        # Activate conda environment
        echo -e "Activating conda environment ... "
        set +u;source activate carve;set -u;

        # This is just to make sure that output folder exists
        mkdir -p $(dirname {output})

        # Move to input folder with GEMs subdir
        cd {input}

        # Run SMETANA detailed
        smetana --flavor cobra -o ../../$(dirname {output})/detailed.tsv -v -d --mediadb ../media_db.tsv -m M11 models/*.xml

        # Create dummy file and return to original dir
        cd ../..
        touch {output}
        """

rule carve:
	input:
		f'models/{{IDs}}/genomes'
	output:
		directory(f'models/{{IDs}}/models')
	message:
		"""
		This rule runs carveme in series for a number of subfolders in parallel
		Note that this is not a practical implementation if gapfilling media is not the same for all communities
		"""
	shell:
		"""
        # Activate conda environment
        echo -e "Activating conda environment ... "
        set +u;source activate carve;set -u;

        # This is just to make sure that output folder exists
        mkdir -p $(dirname {output})

        # Move to input folder with GEMs subdir
        cd {input}

        # Run carveme
        while read model;do     
   			carve -v --mediadb ../media_db.tsv -g M8 --cobra -o ../models/${model}.xml $model;
		done< <(ls|grep faa)

		"""
