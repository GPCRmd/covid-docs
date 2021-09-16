=========
Workbench
=========

.. contents::
    :depth: 2


The Workbench includes a set of online tools for the interactive visualization (*Viewer*) and analysis (*Toolkit*) of individual simulations. It also links the time-resolved protein dynamics with information on existing SARS-CoV-2 variants, their phylogeny, and the corresponding individual isolates. This allows evaluating the structural impact of variants taking into account protein dynamics.


------------------------------
Simulation report and files
------------------------------
By clicking on *Simulation report and files*, you will access the details of the system setup and simulation protocol, as well as links to download the simulation data.


------
Viewer
------

The viewer section of the Workbench page builds on the web-based structure viewer NGL_ 2.00 and MDsrv_ 0.3.5.


Mouse controls
================


* **Left button hold and move**: rotate camera around the center.

* **Middle button hold and move**: zoom camera in and out.
* **Middle button click**: center camera on an atom.
* **Right button hold and move**: translate camera in screen plane.
* **Left button click**: pick atom or distance.

        * When an atom is clicked, a label with information about it appears. Click at the background to deselect it, the label will disappear. To maintain a label, double-click on an atom. Double-click again on the atom to remove the label.

        * To draw a distance line between two atoms just single-click one atom after the other. Distances can be removed by double-clicking on one of the atoms at the edges.

        * It is also possible to remove all the atom labels and distances at once, with the **Clear labels/dists. button**.



Selection tools
===============

Quick selection
---------------

Quick-selection buttons allow to rapidly display or hide the molecules present at the dynamics. Hover the buttons with your mouse to see the abbreviated name of these molecules, if any, which can be used to create your own selections.


Relevant domains
----------------

This section includes a list of relevant domains and annotations present in the protein, extracted from Uniprot_. Select or un-select a domain to represent it on the structure. More information on each domain can be found by clicking on the info button:


* **Seq. position:** Position of the domain in the Uniprot sequence.
* **Seq. (WT):** Wild type sequence of the domain.
* **Selection:** Selection of the domain based on the `NGL selection language`_.
* **Source:** Source Uniprot entry.


Custom selection
----------------

Use the text input field to specify your personalized representations. You can choose a representation type (licorice, cartoon, etc.) and a coloring scheme (color by element, by chain, etc.). Selections must be expressed using the `NGL selection language`_. 



-------
Toolkit
-------

General
======================

Interaction network
---------------------
Interaction network, based on `Flare Plots`_, provides an interactive circular representation of contact networks. Noncovalent residue-residue interactions formed in the simulation are represented as lines connecting residue pairs. Hover or click a residue to highlight the lines representing the interactions in which it participates.

There are several options available

* **Interaction type:** Select the type of interaction to display on the plot.
    * | **Hydrogen bonds:**
      | \|AD| < 3.5Å
      | ∠AHD < 70°
      | Where A (acceptor) and D (donor) are any atom except hydrogen, carbon or sulphur.
    * | **Salt bridges:**
      | \|AC\| < 4.0Å
      | Where:
      | A (anion): ASP/OD1+OD2, GLU/OE1+OE2
      | C (cation): LYS/NZ, ARG/NH1+NH2, HIS/ND1+NE2
      | Based on GetContacts_. 
    * | **Pi-cation:**
      | \|AC| < 6.0Å
      | ∠CAn < 60°
      | Where:
      | A (aromatic): center(PHE/CG+CE1+CE2), center(TRP/CD2+CZ2+CZ3), center(TYR/CG+CE1+CE2), center(HIS/CG+CD2+CE1)
      | C (cation): LYS/NZ, ARG/NH1+NH2, HIS/ND1+NE2
      | Based on GetContacts_.
    * | **Pi-stacking:**
      | \|A1A2| < 7.0Å
      | ∠(n1, n2) < 30°
      | ∠(n1, A1A2) < 45°
      | ∠(n2, A1A2) < 45°
      | Where:
      | A1, A2 (aromatic rings): center(PHE/CG+CE1+CE2), center(TRP/CD2+CZ2+CZ3), center(TYR/CG+CE1+CE2), center(HIS/CG+CD2+CE1)
      | Based on GetContacts_.
    * | **T-stacking:**
      | \|A1A2| < 5.0Å
      | 60° < ∠(n1, n2) < 90°
      | ∠(n1, A1A2) < 45°
      | ∠(n2, A1A2) < 45°
      | Where:
      | A1, A2 (aromatic rings): center(PHE/CG+CE1+CE2), center(TRP/CD2+CZ2+CZ3), center(TYR/CG+CE1+CE2), center(HIS/CG+CD2+CE1)
      | Based on GetContacts_.
    * | **Van der Waals:**
      | \|AB| < Rvdw(A) + Rvdw(B) + 0.5
      | Where A and B are any non-hydrogen atoms.
      | Based on GetContacts_.
    * **Water bridges:** Two different residues forming a Hydrogen bond with the same water molecule. Based on GetContacts_.
    * **Extended water bridges:** Two different residues forming a Hydrogen bond with two different water molecules which also form a hydrogen bond between them. Based on GetContacts_.
    * | **Hydrophobic:**
      | \|AB| < Rvdw(A) + Rvdw(B) + 0.5
      | Where:
      | A, B: ALA+CYS+PHE+GLY+ILE+LEU+MET+PRO+VAL+TRP and element C or S
      | Based on GetContacts_. 

* **Display**:
    * **Interacting pairs**: Allows to filter out interactions formed by residues that are 5 or less residues apart. 
    * **Simulation**: It is possible to summarize the interactions formed through all the trajectory frames. The frequency of each interaction is represented by the thickness of the lines connecting residues.
* **Show in structure**: Click to display structural representations of the residues selected (clicked) at the flare plot. Unclick to hyde them. If there are no residues selected at the flare plot, nothing will happen.
* **Clear plot**: Click to delete all selections made on the plot.
* **Download data**: Click to download the plot data.

Root mean square deviation (RMSD) 
-------------------------------------
This tool computes the RMSD of all the conformations in a target trajectory to a reference conformation using the _rmsd module of MDtraj. If more than one trajectory is available, the user can select the trajectory to be used. Also, it is possible to specify the frames to be considered. The first frame of the trajectory is used as a reference structure by default, but this can be specified by the user. It is also possible to choose which atoms are going to be considered in the calculation: only alpha carbons, non-hydrogen protein atoms, protein C-alpha, etc. Results are shown in a plot (RMSD by time or by frame). It is possible to download the plot as an image or all the obtained data as a CSV file.


Root mean square fluctuation (RMSF)
-------------------------------------
The RMSF is computed for all the alpha carbons of the protein using the rmsf_ module of MDtraj. It is calculated based on the average structure of the simulation, obtained by averaging the coordinates of each atom during the trajectory. The trajectory is aligned to the obtained average structure before the RMSD is calculated.


Variant impact
================
This tool interactively references the MD simulations with information on existing SARS-CoV-2 variants obtained from GISAID_. Each of the variants is annotated with static (mutation-dependent) and time-dependent (computed on the basis of the simulation dynamics) descriptors of their impact on multiple aspects of the protein’s structure, dynamics, and function. By assigning user- or pre-defined weights to these descriptors, the descriptors are combined in an impact score. 

Sequence selector
-------------------
This tool displays the wild-type sequence of the protein or proteins present in the simulation, extracted from Uniprot (residue name and sequence position). Place your mouse on a residue to see the structure residue ID corresponding to that position. Have in mind that the residue ID may not correspond to the Uniprot sequence position. 

Positions that have a known variant are colored in the sequence. It is possible to filter the variants that are displayed on the sequence to show only those present in a particular isolate of interest. This can be done with the **"Isolate"** dropdown.

Click on a position with known variants to highlight it n the structure. Please note that the model may incorporate some mutations with respect to the wild-type sequence, so the residue name of the sequence (wild type) can, in some cases, not correspond to the residue name in the structure. 

When a position with known variants is clicked, a pop-up with the list of variants appears. Click on one of the variants to obtain more information about its descriptors and impact score. 

The **"Display in viewer"** checkbox control whether or not the variant information is displayed at the Viewer. If it is unselected, clicked positions will not be highlighted on the structure, and it will not be possible to color the structure based on the impact score.


Descriptors of variant impact
--------------------------------
Our descriptors include:

* **Mutation effect descriptors**, representing the impact of the amino acid change. Unless indicated otherwise, they were obtained from Biopython_ 1.76.
        * BLOSUM90 score
        * Charge difference, based on the charge of the wild type and mutated amino acid
        * `Epstein's coefficient of difference`_ 
        * `Experimental exchangeability`_
        * `Grantham's distance`_ 
        * `Miyata's distance`_ 
        * `Sneath's index`_ 
        * Several scales of change in hydrophobicity: `Kyte-Doolittle`_, `Eisenberg-Weiss`_ , Engelman_, Hessa_, Hopp-Woods_, Janin_, Moon-Fleming_, Wimley-White_, Zhao-London_
        * Variant effect predictions extracted from the database `Mutfunc SARS-CoV-2`_, including conservation, structural consequences and `experimental antibody escape data`_.
        
* **Time-dependent predictors**, consisting of parameters extracted from the wild type simulation for the residue affected by the variant. They allow us to evaluate the structural impact of each variant. These predictors were obtained from the trajectory strided so that the delta is 0.1 ns or, in longer simulations, 1ns. 
    * RMSD of the residue with relation to the first trajectory frame, obtained using the rmsd_ module of MDtraj.
    * RMSF of the residue atoms, obtained with the rmsf_ module of MDtraj. 
    * Solvent-accessible surface (SASA) of the residue, based on the Shrake and Rupley algorithm, calculated with the shrake_rupley_ algorithm of MDtraj. 
    * Chi1 angle of the residue, which corresponds to the first side chain torsion angle formed between the 4 atoms over the CA-CB axis, if available. The Chi1 angle is calculated using the compute_chi1_ module of MDtraj.
    * Number of contacts that the residue makes with other protein residues, obtained with GetContacts_. This includes hydrogen bonds, salt bridges, hydrophobic contacts, pi-cation contacts, pi-stacking contacts, t-stacking contacts, Van der Waals, water bridges, extended water bridges and total contacts.

  Click on the **+** sign beside each time-dependent predictor to see the value of the predictor by simulation time. By clicking on the plot, the user can set the Viewer to the corresponding trajectory frame.

* | **User-provided descriptors**, which can be provided by the user as a CSV-formatted file, based on the template provided at the top of the section (example here_). Upload the CSV, with comma separated values, using the "Browse" and "Upload" buttons to generate the corresponding sliders.
  | Of note, custom descriptors enable the inclusion of arbitrary external data, as well as non-linearities and interactions, in the prediction models. 


.. _`Epstein's coefficient of difference`: https://doi.org/10.1038/215355a0
.. _`Experimental exchangeability`: doi.org/10.1534/genetics.104.039107
.. _`Grantham's distance`: https://doi.org/10.1126/science.185.4154.862
.. _`Miyata's distance`: https://doi.org/10.1007/BF01732340
.. _`Sneath's index`: https://doi.org/10.1016/0022-5193(66)90112-3
.. _`Kyte-Doolittle`: https://doi.org/10.1016/0022-2836(82)90515-0
.. _`Eisenberg-Weiss`: https://doi.org/10.1016/0022-2836(84)90309-7
.. _Engelman: doi.org/10.1146/annurev.bb.15.060186.001541 
.. _Hessa: https://doi.org/10.1038/nature06387
.. _Hopp-Woods: https://doi.org/10.1073/pnas.78.6.3824
.. _Janin: https://doi.org/10.1038/277491a0
.. _Moon-Fleming: https://doi.org/10.1073/pnas.1103979108
.. _Wimley-White: https://doi.org/10.1038/nsb1096-842
.. _Zhao-London: https://doi.org/10.1110/ps.062286306
.. _`Mutfunc SARS-CoV-2`: http://sars.mutfunc.com/home
.. _`experimental antibody escape data`: https://doi.org/10.1016/j.chom.2020.11.007
.. _shrake_rupley: https://mdtraj.org/1.9.4/api/generated/mdtraj.shrake_rupley.html
.. _compute_chi1: https://mdtraj.org/1.9.4/api/generated/mdtraj.compute_chi1.html
.. _here: https://submission.gpcrmd.org/covid19/dwl/cdescr_template/28

Impact score
-------------------
The descriptors are combined in an impact score, defined as the sum of each weighted descriptor. Users may assign predefined or custom weight combinations to the descriptors to reflect various aspects of the structural impact of the variant. 

Predefined weights can be enabled with buttons in the *Impact score* section that load the corresponding sets of coefficients in the “weight” sliders inside the *Mutation effect* and *Time-dependent* boxes. They include:

* **Model-based weights:** obtained based on regularized regression models (LASSO) trained on 23 per-variant covariates, used as predictors, computed on the basis of the 12 MD trajectories containing the Spike receptor-binding domain (RBD) available at the time of writing. Each of these models was trained to fit the corresponding experimental quantity, measured for each variant in deep scanning mutagenesis experiments. Model-based weights are only available for simulations including the RBD.
    * **Fitted to antibody escape:** trained to estimate, for each variant, its impact in terms of the potential for `antibody evasion`_.
    * **Fitted to binding:** trained to estimate, for each variant, its impact in terms of the change in `binding affinity`_ between the RBD and the ACE2 receptor.
    * **Fitted to expression:** trained to estimate, for each variant, its impact in terms of the change in expression_ of the RBD on yeast cells.
* **Other weights:**
    * **RMSF and contacts:**  weights set to consider, equally, RMSF and all contact types.


.. _`binding affinity`: https://doi.org/10.1016/j.cell.2020.08.012
.. _expression: https://doi.org/10.1016/j.cell.2020.08.012
.. _`antibody evasion`: https://doi.org/10.1016/j.chom.2020.11.007


To set a customized set of weights, the user can manually set the “weight” sliders inside the *Mutation effect* and *Time-dependent* boxes.


If a variant is selected in the *Sequence selector*, the obtained score is presented together with a *q value*, showing its rank in the distribution of all variants (q=0, 0.5, and 1 respectively mean that the selected amino acid variant achieves the minimum, median and maximum effect score with respect to the other ones observed in the available sequences). Also, the distribution of all variants is shown as a histogram, on which the impact score of the selected variant is highlighted. A significant shift of the variant score to the right or left from the distribution peak reflects a variant with a high propensity to disturb protein function based on the selected descriptors.  


Finally, a color scale is generated based on the impact score of the variants in the protein sequence. Both the *Sequence selector* and the protein structure in the Viewer can be automatically colored based on this scale. In residues with more than one variant, the color corresponds to the average score of all the residue variants. 








.. _Uniprot: https://covid-19.uniprot.org
.. _GetContacts: https://getcontacts.github.io/interactions.html
.. _NGL: http://nglviewer.org/ngl/api/index.html
.. _MDsrv: http://nglviewer.org/mdsrv/
.. _gnomAD database: https://gnomad.broadinstitute.org/
.. _GPCRdb: https://www.gpcrdb.org/
.. _NGL selection language: http://nglviewer.org/ngl/api/manual/usage/selection-language.html
.. _wernet_nilson: http://mdtraj.org/1.8.0/api/generated/mdtraj.wernet_nilsson.html
.. _`Flare Plots`: https://doi.org/10.1101/840694 
.. _rmsd: https://mdtraj.org/1.9.4/api/generated/mdtraj.rmsd.html
.. _rmsf: https://mdtraj.org/1.9.4/api/generated/mdtraj.rmsf.html
.. _GISAID: https://www.gisaid.org/
.. _Biopython: https://biopython.org/