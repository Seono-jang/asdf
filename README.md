# Week 2 - Markov Localization

---

[//]: # (Image References)
[plot]: ./markov.gif

## Assignment

You will complete the implementation of a simple Markov localizer by writing the following two functions in `markov_localizer.py`:

* `motion_model()`: For each possible prior positions, calculate the probability that the vehicle will move to the position specified by `position` given as input.
* `observation_model()`: Given the `observations`, calculate the probability of this measurement being observed using `pseudo_ranges`.

The algorithm is presented and explained in class.

All the other source files (`main.py` and `helper.py`) should be left as they are.

If you correctly implement the above functions, you expect to see a plot similar to the following:

![Expected Result of Markov Localization][plot]

If you run the program (`main.py`) without any modification to the code, it will generate only the frame of the above plot because all probabilities returned by `motion_model()` are zero by default.

---

# HW_01 Markov Localizaion

## 자동차공학전문대학원 자동차IT융합 전공 A2020043


**Observer Model

    # Observation model (assuming independent Gaussian)
    def observation_model(landmarks, observations, pseudo_ranges, stdev):
        # Initialize the measurement's probability to one.
        distance_prob = 1.
        
        if len(observations) == len(pseudo_ranges):
            for i in range(len(pseudo_ranges)):
                distance_prob *= norm_pdf(observations[i],pseudo_ranges[i],1)
        else: 
            distance_prob = 0
        return distance_prob




** Motion Model


    def motion_model(position, mov, priors, map_size, stdev):
        # Initialize the position's probability to zero.
        position_prob = 0.0
        
        for i in range(map_size):
            position_prob += norm_pdf(position-i, mov ,stdev)*priors[i]
            
        
        fx = []
        
        for i in range(map_size):
            fx.append(norm_pdf(position-i, mov ,stdev)*priors[i])


\Delta s = s_G - s Δs=sG​−s : Longitudinal distance from destination;

\Delta d = d_G - d_{LC/KL} Δd=dG​−dLC/KL​: The horizontal distance from the destination;

\text{cost} = 1 - e^{- \frac{|\Delta d|}{\Delta s}} cost=1−e−Δs∣Δd∣
