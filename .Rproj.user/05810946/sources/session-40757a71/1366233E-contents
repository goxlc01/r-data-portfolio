library(tidyverse)

micro_world <-
  read_csv("/Users/cheng128/Documents/UofT/Misc./U-Mich/CodingR/GlobalFindex/micro_world.csv")

# ---- Overall account ownership by economy ----
# For each economy (country), calculate the weighted percentage of adults who have an account
micro_world_account <- 
  micro_world %>%
  group_by(economycode) %>%
  summarise(account = 100 * weighted.mean(account, w = wgt))

wb_income <- 
  read_csv("/Users/cheng128/Documents/UofT/Misc./U-Mich/CodingR/GlobalFindex/wb_income.csv")

# ---- Combine micro-level account data with World Bank income categories ----
account_by_income <- 
  left_join(micro_world_account, wb_income)

# Reorder & relabel income groups to match the figure
account_by_income <- account_by_income %>%
  mutate(
    income_category = factor(
      income_category,
      levels = c("4High", "3UpperMid", "2LowerMid", "1Low"),
      labels = c("High-income economies",
                 "Upper-middle-income economies",
                 "Lower-middle-income economies",
                 "Low-income economies")
    )
  )

# ---- Create a scatter plot showing account ownership by income category ----
ggplot(account_by_income, aes(x = account, y = income_category)) +
  geom_point(aes(fill = income_category),
               shape = 21, size = 3.0, stroke = 1.1, color = "white",
             position = position_jitter(height = 0.05, width = 0)) +
  scale_x_continuous(limits = c(0, 102), breaks = seq(0, 100, 20), expand = c(0, 0)) +
  scale_fill_manual(values = c(
    "High-income economies"            = "#7EC1C9",
    "Upper-middle-income economies"    = "#C7552E",
    "Lower-middle-income economies"    = "#F0B429",
    "Low-income economies"             = "#0C5A85"
  )) +
  labs(
    title = "Account ownership differs substantially even within income groups",
    subtitle = "Adults with an account (%), 2017",
    x = NULL, y = NULL
  ) +
  theme_minimal(base_size = 14) +
  theme(
    legend.position = "none",
    panel.grid.major.x = element_blank(),
    panel.grid.minor = element_blank(),
    plot.background     = element_rect(fill = "white",  color = NA),
    panel.background    = element_rect(fill = "gray98", color = NA),
    plot.margin         = margin(20, 40, 20, 40),
    axis.text.y = element_text(margin = margin(r = 15)),
    plot.title.position = "plot"
  )

# --- Save file ----
ggsave("Final/Account_Ownership.png",
       width = 10, height = 6)