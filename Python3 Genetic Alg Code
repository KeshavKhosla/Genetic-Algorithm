from fuzzywuzzy import fuzz
import random
import string



class Agent:
    
    
    def __init__(self, length):
        
        self.fitness = -1  #Allows us to compare individuals abilities and assigns a 'rating' of sorts -- agents w/ higher fitness scores allows them to move to the next generation; placed as '-1' since evalaution is yet to take place
        self.string = ' '.join(random.choice(string.ascii_letters) for _ in range(length)) # Randomly picks a letter from the alphabet (for a particular length) using the random function previously imported and then joins the string list together
    
    def __str__(self): #printing metadata for each person 

        return 'String: ' + str(self.string) + ' Fitness: ' + str(self.fitness)   
    
'''
Global data that specifies the scope of the project

'''

in_str = None
in_str_len = None
population = 20
generations = 1000


def geneticAlgorithm():
    
    
    agents = init_agents(population, in_str_len)

    for generation in range(generations):

        print ('Generation: ' + str(generation))

        agents = fitness(agents)  #These are the 4 primiary agents of the genetic alg
        agents = selection(agents)
        agents = crossover(agents)
        agents = mutation(agents)

        if any(agent.fitness >= 80 for agent in agents):

            print ('Threshold met!')
            return


def init_agents(population, length):

    return [Agent(length) for _ in range(population)]

def fitness(agents):

    for agent in agents:

        agent.fitness = fuzz.ratio(agent.string, in_str)

    return agents


def selection(agents):

    agents = sorted(agents, key=lambda agent: agent.fitness, reverse=True)
    print ('\n'.join(map(str, agents)))
    agents = agents[:int(0.2 * len(agents))]

    return agents


def crossover(agents):

    offspring = []

    for _ in range(int((population - len(agents)) / 2)):

        parent1 = random.choice(agents)
        parent2 = random.choice(agents)
        child1 = Agent(in_str_len)
        child2 = Agent(in_str_len)
        split = random.randint(0, in_str_len)
        child1.string = parent1.string[0:split] + parent2.string[split:in_str_len]
        child2.string = parent2.string[0:split] + parent1.string[split:in_str_len]

        offspring.append(child1)
        offspring.append(child2)

    agents.extend(offspring)

    return agents


def mutation(agents):

    for agent in agents:

        for idx, param in enumerate(agent.string):

            if random.uniform(0.0, 1.0) <= 0.1:

                agent.string = agent.string[0:idx] + random.choice(string.ascii_letters) + agent.string[idx+1:in_str_len]

    return agents


if __name__ == '__main__':

    in_str = 'GeneticAlgorithm'
    in_str_len = len(in_str)
    geneticAlgorithm()
