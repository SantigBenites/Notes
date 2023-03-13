
# Introduction

- Over view of paper and its objectives

This presentation will be about *_Secure State Estimation and Control of Cyber-Physical Systems: A Survey*, its motivation and main takeaways.
This paper intends in giving an overview of the current state of affairs regarding the usage of both Secure State Estimation and Secure Control when applied to CPS, moreover it analyses possible ways of how SSE & SC can be implemented and used to defend against some of the most common attacks that plague CPS networks.


# Background

- Explain importance of security in CPS
- Explain importance of Secure state estimation of CPS's
- Give examples of possible attacks on CPS
- Give examples of attacks on real systems

Security as a concept is essential to CPS's, however the problems such as the complex mathematical models added to the dynamical models of CPS networks, the inherent complexity added by the close relationship between hardware and software, among others. Lead to ever increasing problems when trying to tackle this situation
- The combination of the occurring cyber attack with the normal uncertainty of the CPS (resulting from delays,data losses, ...) leads to less reliable data about the current state of the system.
- Lack of effective integration of detection algorithms with CPS systems.
- Cascading consequences of the attack propagating through the network.
- Varying network topology due to “plug-and-play” and scalability.
- Inherent complexity of security algorithms and networks topology leads to ever increasingly complex solutions for security in CPS's 

To this effect,  the authors present one of the possible solutions to solving the security problems of  CPS's, the combination of secure state estimation (SSE) and secure control (SC).

In secure state estimation the system defends itself from cyber attacks by trying to maintain proper operation of the system, he does this by making informed decision about its behaviour taking into consideration the environment the CPS is in. In these cases the CPS is therefore represented by a set of values representing different attributes of the system, and the main goal of security wont be to defend against attacks but to keep the system values at the level required for operation.
To maintain the levels at an acceptable level the CPS will resort to using multiple security countermeasures.

To better understand the function of SSE, we must also see that CPS's are usually subjective to 2 types of attacks
- Denial-of-service (DoS) attacks
- Deception attacks
Taking this into account the main appeal of SSE is that it is particularly good at mitigating the effects of both of these types of attacks, by incorporating security into the estimation process.

SC is the inverse process of SSE, while SSE refers to the security of communication between the sensors to the control systems, SC refers the security of communication between the control systems and the sensors.
In other words, SC refers to the process of ensuring the integrity and confidentiality of the control signals used to operate the system.
These are useful because they mitigate the effect of cyber attacks upon the control systems, and allow for another level of security and integrity in the encompassing CPS

# Approaches to Security

- Secure State Estimation Approaches
	- Variance-Based Secure State Estimation
	- Stability-Based Secure State Estimation

- Secure Control Approaches
	- Centralised Secure Control
	- Distributed Secure Control
	- Resource-Aware Secure Control

The authors now review 2 of the possible implementations of SSE


In variance-based SSE, we use the variance of the sensors measurements in the network, with the intent of trying to decide whether there might be an attack is occurring or not. This is done by permanently checking to see if the variance of the sensors surpasses a certain threshold. This approach does have one draw back, it requires structured information of cyber attacks, such as statistical information, as a priori knowledge.
As indicated in the paper, this algorithms is particularly vulnerable to situations where it cant reliably trust the data given by the sensors, deception attacks, this because the only information it gets from the system is the direct values from the sensors. Taking this into account the authors propose some mechanisms to mitigate this flaw
- like turning some sensors into detection mechanisms to evaluate sensors that might be giving out compromised data 
- or using probabilistic models to evaluate the probability that some sensor might have been compromised
While these strategies are useful in a complete network they suffer in situations where only a subset of the system is attacked, and in which the values of variance in the network are not altered in high enough levels as to warrant a response, this can be mitigated by subjecting parts of the network to the algorithm.

In stability-based SSE, we analyse the network to search for deviance from a stable status, with the assumption that if the network deviates from stability, this deviation can be consequence of an attack. The main advantage of this approach is that by focusing on the stability of the system we are less likely to be fooled by possible deception attacks that change sensors in subtle ways, considering we are not focused on sensor values but in stability characteristics. 
In the paper the authors present 2 way of developing this type of approach
- Attack isolation
- Attack attenuation
Attack isolation involves detecting and isolating the components of the system that have been affected by an attack. The goal of attack isolation is to prevent the attacker from influencing the state estimation of the system by limiting the impact of the attack to a subset of the components of the system.
Attack attenuation involves reducing the impact of an attack on the state estimation by minimising the effect of the attack on the system. The goal of attack attenuation is to prevent the attacker from influencing the state estimation of the system by reducing the impact of the attack on the measurements used for state estimation.
As indicated in the paper, this approach suffers from a similar problem to the past one, where if the system cant trust the values of the stability values it cant properly conduct its purpose, for this effect the authors present the usage of saturated models(https://en.wikipedia.org/wiki/Saturated_model, acho que e isto) as a possible way to solve this situation.
Regardless, the dual relationship between stable and unstable can be exploited by attackers to be able to find a tolerable range of attack in which they can try to break the system, alterations to the stability function can be made to diminish the risk.


While both systems have their upsides and downsides
- variance-based SSE is better for systems that require fast response times and high accuracy.
- stability-based SSE is better for systems that require robustness and resilience in the face of attacks.

The authors mainly focus on 3 types of secure control

Centralised Secure Control is a type of SC where the CPS is controlled by a single entity. In this type the CPS controls are made the central control and the sensors and actuators only provide feedback the central entity.
This approach provides multiple advantages
- Simplified control structure
- Improved performance
- Simpler security management
but also has multiple disadvantages
- Single point of failure
- Increased communication overhead

The authors refer, that in order for this system to be able to be used in the situation of DOS attacks it must work in a way that the central control cant be overwhelmed, for this they refer to a mode in which the central controls work in a open-loop manner, by this they refer to the system permanently outputting controls in a fixed timescale, like a pendulum/monotone. This allows the central control to even in the situation of DOS attack continue on giving out orders.
Moreover, the authors refer that while this mode of operation leads to easier security than its alternatives, it can be easily read and analysed by attackers leading to them having an easier time in trying to exploit it. This one the other hand, gives the central control more leverage on the attackers by being simpler for the control to accurately access attacks and being easier for it to get all necessary information for future countermeasures. Both these facts lead to am interesting game theory analysis of how the non-cooperative game between the attackers and defenders works in the specific architecture.

Distributed Secure Control is a type of SC where the CPS is controlled by a distributed set of entities. In this type certain agents are responsible by sets of sensors and to generate controls for their sensors, each of these agents is responsible to coordinated its controls with the other agents.
This approach provides multiple advantages
- Increased robustness
- Increased flexibility
- Reduced communication overhead
but also has multiple disadvantages
- Increased complexity
- Increased security management

The authors refer that, while the location disparity of the control central can lead to a broader attack surface and less security in general, the majority of the downside can be suppressed with proper implementation of some techniques in the sensors and control nodes.
For this effect they refer that
- While unlike Centralised Secure Control , there isn't a single entity responsible for sending out order to the CPS and therefore there isn't a single entity that needs to evaluate the CPS for possible attack information, an alternative approach can be collect attack information in each group agent, and use the collective of the group agent to collective analyse the data and decide over the attack information, while this approach is effective and results in some attack attenuation, it is more constantly that its centralised counter part.
- Expectantly this approach can be more resilient to DDOS attacks, considering multiple points of control can lead to no single node being possibly crucial to control the entire CPS.
- The multiple control nodes distrusted around the CPS, allow for an interesting effect where the different control nodes have different control responsibilities in the CPS, allowing for not only robustness and scalability of the network but also for better attack defence and mitigation of attack influence. _Take for example a network where a distributed state predictor is employed to estimate the existing  attacks, and then a resilient controller is designed to guarantee robust performance and to adaptively compensate for the influence of attack_ (apenas dizer se tiver tempo)

Resource-Aware Secure Control is a type of SC where the CPS is controlled by algorithms that take resource management into account when creating controls. These algorithms are designed to optimise the system from both a security and resource utilisation point of view. This allows for the system to operate in a way that is not only secure but also efficient from a resource stand point.
This approach provides multiple advantages
- Improved performance
- Reduced resource requirements
- Improved security
but also has multiple disadvantages
- Trade-offs between security and resource utilisation
- Increased complexity

On one hand, the authors point out that this approach results in decreases system performance/complexity, this results from the fact that the sensors/actuators will need adopt a feedback control system, not only for the original data but also for resource management, which will inevitably lead to bigger loads on the connections.
On the other hand, the authors also refer some possible solutions to the main problems of this methodology
- During the course of an attack it is common that the system can have some leeway regarding the timing in which it needs to deploy countermeasures, for this purpose the author refers that in order to upgrade the system an possibility better attack mitigation it proposes using Lypanov function to calculate how long the system will stay stable and even calculate a maximum downtime that wont make the system run out of resources. Allowing to predict possible max times of attack, and how long the system as to fix the current situation with countermeasures
- In a general perspective, this type of approach makes trade-offs between detection precision and resource control performance, taking this into account a well implemented attack detection and secure control can go a long way into improving the general performance of the methedology. It is therefore paramount that when trying to use this approach we plan acceptable security performance and desirable control performance beforehand.

(==Aqui se calhar podia ser bom falar mais em comparações diretas entre eles, por exemplo dizer logo que distributed é mais complexo que centralizado, falar tb de coisas variadas==, **dado que no paper eles nao os comparam diretamente acho que refirir o que os autores pensam adicionar sobre cada metodologia/algoritmo e capaz de ser melhor**) btw se quiseres adiciona aquela parte dos exemplos mas ja estam demasiadas palavras



# Conclusion

- Summarise the research paper
- Identify open research questions
- Reinforce the message of the paper

The research paper "Secure State Estimation and Control of Cyber-Physical Systems: A Survey" provides an overview of the existing literature on the secure control and estimation of cyber-physical systems (CPS) in the presence of cyber-attacks.
The paper discusses the challenges posed by cyber-attacks on the security and safety of CPS and surveys the different approaches proposed to address these challenges.

The authors also present some unanswered questions which they believe to be relevant to future works
- How to the physical location of sensors and actuators can affect cyber security in a CPS
- How plug-and-play can affect the cyber security needs of a CPS and its SSE and SC
- How artificial intelligence can affect SSE and SC in future CPS's