# 🎮 Prisoner's Dilemma in Financial Markets
### A Game Theory Simulation — Strategy vs. Greed

---

## What is This Project?

This is a Python-based simulation of the **Prisoner's Dilemma** — one of the most famous concepts in game theory — applied to the context of **financial markets**.

The core idea is simple: two players (think of them as competing firms or traders) each independently decide whether to **Cooperate** or **Defect**. Their payoffs depend on what *both* players choose — not just their own decision. The catch? Acting purely in self-interest leads to an outcome that's worse for everyone.

This project simulates what happens when different strategies play against each other across 100 rounds, runs a full round-robin tournament, and visualizes the results.

---

## The Financial Interpretation

In financial markets, this maps directly to real-world behavior:

| Game Action | Financial Meaning |
|---|---|
| **Cooperate** | Maintain fair pricing, prudent risk-taking, honest information sharing |
| **Defect** | Predatory pricing, excessive risk, withholding information for short-term gain |

The Prisoner's Dilemma explains phenomena like **price wars**, **collusion**, **excessive leverage**, and **herd behavior** in markets — situations where individually rational decisions lead to collectively terrible outcomes.

---

## The Payoff Matrix

Every round, two players pick C (Cooperate) or D (Defect). Payoffs are:

```
              Opponent: C       Opponent: D
Our move: C   (3, 3) Reward     (0, 5) Sucker
Our move: D   (5, 0) Temptation (1, 1) Punishment
```

- **Both Cooperate (3, 3):** Stable market — both firms earn steady profits
- **You Defect, They Cooperate (5, 0):** You exploit them for a big short-term win
- **You Cooperate, They Defect (0, 5):** You get wiped out; they gain
- **Both Defect (1, 1):** Mutually destructive price war — both lose

The dilemma: Defecting always looks better *individually* in the moment. But if both players think this way, they both end up with 1 instead of 3. This is the tragedy of the Prisoner's Dilemma.

---

## The 6 Strategies Tested

Each strategy models a different type of market participant:

**Always Cooperate** — Never defects. Represents an idealistic firm committed to ethical behavior at all times.

**Always Defect** — Never cooperates. The pure opportunist — exploits every interaction for short-term gain.

**Random** — Chooses C or D with 50% probability each round. Models unpredictable or irrational market behavior.

**Tit for Tat** — Starts by cooperating. Then mirrors whatever the opponent did last round. Nice, retaliatory, and forgiving. The most famous strategy in iterated PD research.

**Grudger (Grim Trigger)** — Cooperates until the opponent defects even once, then defects forever. "Once burned, twice shy." Common in long-term business relationships after a betrayal.

**Pavlov (Win-Stay, Lose-Shift)** — If the last round went well, repeat the same action. If it went badly, switch. A simple reinforcement-learning style approach.

---

## How the Simulation Works

1. **One-Shot Game** — First, a single round is simulated to demonstrate the basic dilemma.
2. **Repeated Game** — Two strategies play 100 rounds against each other, building up history. Strategies can adapt based on past behavior.
3. **Round-Robin Tournament** — Every strategy plays every other strategy (and itself) for 100 rounds. Total and average payoffs are tracked.
4. **Visualizations** — Results are plotted across multiple charts to reveal patterns.

---

## Output & Results

### 🏆 Tournament Payoff Leaderboard

![Payoff Leaderboard](https://github.com/arham7s/Prisoner-s-Dilemma-in-Financial-Markets/blob/main/output/Payoff%20leaderboard%20bar%20chart.png)

Counterintuitively, **Always Defect** tops the leaderboard in mean payoff per round (2.66), followed by **Grudger** (2.63) and **Tit for Tat** (2.46). Always Cooperate and Random sit at the bottom.

This makes sense in a mixed tournament — defecting strategies earn big against naive cooperators. But this doesn't mean defecting is the "right" strategy in real markets; it just means that cooperating strategies are vulnerable *when the opponent pool includes exploitative strategies*.

---

### 🤝 Cooperation Rate by Strategy

![Cooperation Rate](https://github.com/arham7s/Prisoner-s-Dilemma-in-Financial-Markets/blob/main/output/Cooperation%20rate%20by%20strategy.png)
- **Always Cooperate**: 100% cooperation (by definition)
- **Pavlov**: ~80% — adapts and cooperates when rewarded
- **Tit for Tat**: ~71% — mirrors opponents, so cooperation rate depends on who it faces
- **Grudger**: ~61% — holds out cooperating until first betrayal
- **Random**: ~55% — close to the 50% expected by random chance
- **Always Defect**: 0% cooperation (by definition)

---

### 📊 Tournament Payoff Heatmap

![Tournament Heatmap](https://github.com/arham7s/Prisoner-s-Dilemma-in-Financial-Markets/blob/main/output/Tournament%20payoff%20heatmap.png)

This heatmap shows what each strategy *earns* when facing each opponent:

- **Always Defect vs Always Cooperate** is the highest-earning matchup (5.00) — the defector fully exploits the cooperator
- **Always Cooperate vs Always Defect** is the worst (0.00) — sucker payoff every round
- **Symmetric strategies** (TfT vs TfT, Grudger vs Grudger, Pavlov vs Pavlov) cluster around 3.00 — mutual cooperation maintained
- Always Defect earns only 1.04 against Tit for Tat and Grudger — they retaliate and punish, locking in the mutual punishment payoff

---

### 📈 Cumulative Payoff: Tit for Tat vs Always Defect

![Cumulative Payoff](https://github.com/arham7s/Prisoner-s-Dilemma-in-Financial-Markets/blob/main/output/Cumulative%20payoff%20over%20rounds%20(Tit%20for%20Tat%20vs%20Always%20Defect).png)

Always Defect edges out Tit for Tat in cumulative payoff because it exploits the very first round (TfT cooperates round 1, gets suckered), and then both strategies defect every round after. The gap never widens — it's just that initial first-round exploitation that gives Always Defect a persistent but small lead.

This illustrates why **first-mover trust** is so costly: once exploited, TfT retaliates indefinitely and cooperation never recovers.

---

### 🔁 Action History: Cooperate vs Defect Over Time

![Action History](https://github.com/arham7s/Prisoner-s-Dilemma-in-Financial-Markets/blob/main/output/Action%20history%20(Cooperate%20vs%20Defect%20over%20time).png))

Tit for Tat cooperates in round 1, gets defected on, then defects for all remaining 99 rounds. Always Defect never cooperates. The result: a permanent mutual defection equilibrium from round 2 onwards.

This is the classic **defection trap** — once trust breaks, it never comes back in a simple two-player setting.

---

## Key Takeaways

**One-shot games → always defect.** When there's no future, there's no incentive to cooperate. This is why anonymous or one-time financial transactions (like dark pool trades) tend to see more aggressive behavior.

**Repeated interactions enable cooperation.** When players expect to face each other again, the threat of future retaliation makes cooperation rational. This is why long-term institutional relationships tend to be more stable.

**Tit for Tat works best in cooperative environments.** It loses to pure defectors head-to-head but creates sustainable mutual cooperation against other "nice" strategies. In a world full of defectors, it suffers.

**Always Defect wins short-term, loses long-term.** In a tournament with diverse strategies, defectors score high by exploiting cooperators — but as cooperators get weeded out or adapt, defectors are stuck punishing each other.

**Market stability ≈ cooperative equilibrium.** When firms, banks, or traders maintain cooperative norms (fair pricing, reasonable risk), everyone earns steady payoffs. Defection (excessive leverage, predatory pricing) can pay off individually but destabilizes the whole system.

---

## Tech Stack

- **Python 3** — Core simulation logic
- **NumPy & Pandas** — Data manipulation and payoff calculations
- **Matplotlib & Seaborn** — All visualizations
- **Google Colab** — Development environment

---

## File Structure

```
├── Prisoner's_Dilemma_Financial_Markets.ipynb   # Main notebook
├── README.md                                     # This file
├── Payoff_leaderboard_bar_chart.png
├── Cooperation_rate_by_strategy.png
├── Tournament_payoff_heatmap.png
├── Cumulative_payoff_over_rounds_(TfT_vs_Always_Defect).png
└── Action_history_(Cooperate_vs_Defect_over_time).png
```

---

## Running It Yourself

1. Clone the repo or download the `.ipynb` file
2. Open in Google Colab or Jupyter Notebook
3. Run all cells top to bottom
4. Modify `player_a_action` and `player_b_action` in the one-shot cell to try different combinations
5. Change `num_rounds` in the repeated game cells to experiment with longer or shorter horizons

No external APIs needed. All libraries are standard and available in Colab by default.

---

## Further Reading

- Axelrod, R. (1984). *The Evolution of Cooperation* — the foundational book on iterated PD tournaments
- Axelrod & Hamilton (1981). *The Evolution of Cooperation* — Science paper showing TfT's dominance
- Shiller, R. (2015). *Irrational Exuberance* — on how market psychology and coordination failures link to PD dynamics

---

*Built as part of a quantitative finance + game theory exploration. April 2026.*
