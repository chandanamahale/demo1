class Job:
    def __init__(self, job_id, deadline, profit):
        self.job_id = job_id
        self.deadline = deadline
        self.profit = profit


def job_scheduling(jobs):
    # Sort jobs in DESCENDING order of profit
    jobs.sort(key=lambda x: x.profit, reverse=True)

    print("\nJobs in Descending Order of Profit:")
    for job in jobs:
        print(f"Job ID: {job.job_id}, Deadline: {job.deadline}, Profit: {job.profit}")

    # Find maximum deadline
    max_deadline = max(job.deadline for job in jobs)

    # Create time slots
    slots = [None] * (max_deadline + 1)
    total_profit = 0

    # Greedy scheduling
    for job in jobs:
        for t in range(job.deadline, 0, -1):
            if slots[t] is None:
                slots[t] = job.job_id
                total_profit += job.profit
                break

    scheduled_jobs = [job for job in slots if job is not None]
    return scheduled_jobs, total_profit


# ----------- User Input -----------

n = int(input("Enter number of jobs: "))
jobs = []

for i in range(n):
    print(f"\nEnter details for Job {i+1}")
    job_id = input("Job ID: ")
    deadline = int(input("Deadline: "))
    profit = int(input("Profit: "))
    
    jobs.append(Job(job_id, deadline, profit))

scheduled_jobs, total_profit = job_scheduling(jobs)

print("\nScheduled Jobs:", scheduled_jobs)
print("Total Profit:", total_profit)
