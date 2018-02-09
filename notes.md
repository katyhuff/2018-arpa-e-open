### Concept Summary 

The method that we are investigating has the possibility of exploring the
improvement of Monte Carlo radiation transport by leveraging machine learning methods.
Monte Carlo radiation transport methods have classically been improved by reducing runtime
by tracking "important" particles in the system and reducing the population of
"unimportant" particles in the system. Importance is defined
based on the method, but is often obtained directly from a
transport code. Our method will apply machine learning techniques to Monte
Carlo radiation transport to update Monte Carlo importances based on machine
learning algorithms. This potentially could be applied to both shielding and
reactor calculations, and limits the need for multiple transport codes.
Further, the user would not be required to have detailed knowledge of choosing
optimal deterministic parameter choices to aid in variance reduction. The ML
algorithm would choose these parameters based on a set number of MC cycles.   

### Innovation and impact

### Proposed Work

* Developing a piece of software that updates MC weight window maps based on ML
  methods. 
* Exploratory study on the optimal number of particles to run, the number of
  iterations of MC that we might do while updating WW values


### Team Organization and Capabilities


### Thoughts

* to use a previous MC iteration to set the importances in the next calculation
  we need to tally in MC
  * how do we want to tally? Do we want to bypass it altogether?
    * If we want to bypass it altogether then we would have to modify OpenMC. 
      * WW map would be defined in dimensions based on whatever algorithm we
        get based on particle tracking
      * Potentially a lot of I/O pulling particle tracking information to
        determine optimal ww vals (in space, energy and angle) 
      * Potentially also the most game-changing because we don't need to tally
        in MC at all, so we're not necessarily limited by tally statistics in
        the same way. 
      * We are still limited by the problem physics themselves (particles may
        not be able to penetrate material. This might influence the number of
        iterations we need to converge on a "good" WW map.
    * If we tally then we can build everything in PyNE 
      * We can think of a WW map as a mesh that sets limits on the particle
        weights (both upper and lower bounds). 
      * If we tally over a mesh in the problem then we can generate a WW map
        that matches the tally dimensions
  * need to think about how regions with low tally results might have a lot of
    noise
  * most of the time importance is synonymous with the adjoint solution to the
    problem. Do we want to use this? Or do we want to define our own
    importance? 
* Instead of doing SB we could use ML to generate a source distribution in
  eigenvalue calc in addition to the WWs. 

### To discuss:
* Difference between defining source distribution in MC vs. source biasing in
  fixed source calc. How we leverage MC for either/both. 

