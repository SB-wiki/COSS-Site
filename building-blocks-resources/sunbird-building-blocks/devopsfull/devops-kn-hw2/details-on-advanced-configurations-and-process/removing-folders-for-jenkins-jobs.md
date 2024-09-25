---
icon: elementor
---

# Removing folders for Jenkins jobs

1\. If you decide to purge some environment or no longer require Jenkins jobs for this environment, the process to update Jenkins jobs is quite simple.\
2\. Follow the same steps as mentioned in Creating new folders for Jenkins jobs\
3\. Instead of adding a new entry, just remove the environment you don’t require from the **envOrder.txt** file and update the order number (0,1,2 etc)\
4\. Example:

_**Before Purge**_

| <p><strong>dev=0</strong><br><strong>pre-production=1</strong><br><strong>production=2</strong></p> |
| --------------------------------------------------------------------------------------------------- |

_**After Purge**_

| <p><strong>dev=0</strong><br><strong>production=1</strong></p> |
| -------------------------------------------------------------- |

5\. Run the **jenkins-jobs-setup.sh** script as before and it will update the job configuration accordingly.\
6\. Manually go and remove the pre-production directory from Jenkins UI if required.
