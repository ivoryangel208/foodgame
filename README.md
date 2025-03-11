import javax.swing.*;
import java.awt.*;
import java.awt.event.*;
import java.util.Random;

public class PlantGame extends JFrame implements ActionListener {
    // Game Constants
    private static final int SCREEN_WIDTH = 800;
    private static final int SCREEN_HEIGHT = 600;
    private static final String[] STAGES = {"🌱 Seed", "🌿 Sprout", "🌳 Vegetative", "🌸 Flowering", "🍇 Harvest"};
    private static final Color[] WEATHER_COLORS = {Color.CYAN, Color.GRAY, Color.YELLOW};  // Rain, Storm, Sunny
    private static final int MAX_STRANDS_COUNT = 3;  // Maximum strains in the game

    // Strain Names
    private static final String[] STRAINS = {"Blue Dream", "OG Kush", "Gelato", "Pineapple Express", "Granddaddy Purple"};

    // Plant Attributes
    private Plant plant;
    private Random random;
    private Timer gameTimer;
    private boolean miniGameActive;

    // UI Components
    private JLabel plantInfoLabel;
    private JLabel weatherLabel;
    private JLabel achievementLabel;
    private JPanel gamePanel;
    private JButton waterButton, growButton, fertilizeButton, harvestButton, createEdibleButton, rollJointButton, dabButton;

    // Strain Collection
    private java.util.List<Strain> strains;

    public PlantGame() {
        setTitle("Ultimate Plant Grower 🌱");
        setSize(SCREEN_WIDTH, SCREEN_HEIGHT);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new BorderLayout());

        // Plant Initialization
        plant = new Plant();
        random = new Random();
        strains = new java.util.ArrayList<>();

        // Create Strains
        for (int i = 0; i < MAX_STRANDS_COUNT; i++) {
            strains.add(new Strain(STRAINS[i], random.nextInt(10) + 1, random.nextInt(100) + 1));
        }

        // Set up the game panel
        gamePanel = new JPanel() {
            @Override
            protected void paintComponent(Graphics g) {
                super.paintComponent(g);
                // Draw background based on weather
                g.setColor(WEATHER_COLORS[random.nextInt(WEATHER_COLORS.length)]);
                g.fillRect(0, 0, SCREEN_WIDTH, SCREEN_HEIGHT);

                // Draw strains
                g.setColor(Color.WHITE);
                g.drawString("Strains Available: ", 10, 50);
                for (int i = 0; i < strains.size(); i++) {
                    g.drawString(strains.get(i).getName() + " (Health: " + strains.get(i).getHealth() + "%)", 10, 70 + i * 20);
                }

                // Draw plant
                g.setColor(plant.getColor());
                g.fillRect(300, 200, plant.getWidth(), plant.getHeight());

                // Display plant status
                g.setColor(Color.WHITE);
                g.drawString("Stage: " + STAGES[plant.getStage()], 10, 200);
                g.drawString("Health: " + plant.getHealth() + "%", 10, 230);
                g.drawString("Water: " + plant.getWaterLevel() + "%", 10, 260);
                g.drawString("Growth Time: " + plant.getGrowthTime() + "s", 10, 290);
            }
        };
        gamePanel.setPreferredSize(new Dimension(SCREEN_WIDTH, SCREEN_HEIGHT));
        add(gamePanel, BorderLayout.CENTER);

        // Set up info panel
        JPanel infoPanel = new JPanel();
        plantInfoLabel = new JLabel("Welcome to Plant Grower 🌱");
        weatherLabel = new JLabel("Weather: Sunny");
        achievementLabel = new JLabel("Achievements: None yet");

        infoPanel.setLayout(new GridLayout(4, 1));
        infoPanel.add(plantInfoLabel);
        infoPanel.add(weatherLabel);
        infoPanel.add(achievementLabel);
        add(infoPanel, BorderLayout.NORTH);

        // Buttons for interaction
        waterButton = new JButton("Water Plant");
        growButton = new JButton("Grow Plant");
        fertilizeButton = new JButton("Fertilize Plant");
        harvestButton = new JButton("Harvest Plant");
        createEdibleButton = new JButton("Create Edible");
        rollJointButton = new JButton("Roll Joint");
        dabButton = new JButton("Take Dab");

        waterButton.addActionListener(this);
        growButton.addActionListener(this);
        fertilizeButton.addActionListener(this);
        harvestButton.addActionListener(this);
        createEdibleButton.addActionListener(this);
        rollJointButton.addActionListener(this);
        dabButton.addActionListener(this);

        JPanel buttonPanel = new JPanel();
        buttonPanel.add(waterButton);
        buttonPanel.add(growButton);
        buttonPanel.add(fertilizeButton);
        buttonPanel.add(harvestButton);
        buttonPanel.add(createEdibleButton);
        buttonPanel.add(rollJointButton);
        buttonPanel.add(dabButton);
        add(buttonPanel, BorderLayout.SOUTH);

        // Start game timer to simulate plant growth over time
        gameTimer = new Timer(1000, e -> updateGame());
        gameTimer.start();
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        if (e.getSource() == waterButton) {
            plant.water();
            updateAchievement("Watered plant!");
        } else if (e.getSource() == growButton) {
            plant.grow();
            updateAchievement("Plant grew!");
        } else if (e.getSource() == fertilizeButton) {
            plant.fertilize();
            updateAchievement("Fertilized plant!");
        } else if (e.getSource() == harvestButton) {
            if (plant.getStage() == 4) { // Only harvest if plant is fully grown
                plant.harvest();
                updateAchievement("Harvested plant!");
            }
        } else if (e.getSource() == createEdibleButton) {
            createEdible();
            updateAchievement("Created Edible!");
        } else if (e.getSource() == rollJointButton) {
            rollJoint();
            updateAchievement("Rolled a Joint!");
        } else if (e.getSource() == dabButton) {
            takeDab();
            updateAchievement("Took a Dab!");
        }
        repaint();  // Repaint the screen to show updated plant status and strains
    }

    private void updateGame() {
        // Simulate growth and decay
        plant.passTime();
        repaint();
    }

    private void updateAchievement(String message) {
        achievementLabel.setText("Achievements: " + message);
    }

    private void createEdible() {
        String edibleType = "CBD Edible";  // Create a basic edible
        JOptionPane.showMessageDialog(null, "You have created a " + edibleType + "!");
    }

    private void rollJoint() {
        JOptionPane.showMessageDialog(null, "You rolled a Joint with the finest strain!");
    }

    private void takeDab() {
        JOptionPane.showMessageDialog(null, "You took a Dab!");
    }

    // Start the game
    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> new PlantGame().setVisible(true));
    }

    // Inner class to represent a strain
    class Strain {
        private String name;
        private int growthSpeed;  // Speed at which the strain grows
        private int health;  // Health of the strain

        public Strain(String name, int growthSpeed, int health) {
            this.name = name;
            this.growthSpeed = growthSpeed;
            this.health = health;
        }

        // Getters
        public String getName() {
            return name;
        }

        public int getGrowthSpeed() {
            return growthSpeed;
        }

        public int getHealth() {
            return health;
        }

        public void setHealth(int health) {
            this.health = health;
        }
    }

    // Inner class to represent a plant
    class Plant {
        private int stage;
        private int health;
        private int waterLevel;
        private int growthTime; // in seconds

        public Plant() {
            this.stage = 0;  // Initial stage: Seed
            this.health = 100;  // Start with 100% health
            this.waterLevel = 100;  // Start with full water
            this.growthTime = 0;
        }

        // Plant actions
        public void water() {
            waterLevel = Math.min(100, waterLevel + 10);  // Watering increases water level by 10%
            if (waterLevel >= 100) health = Math.min(100, health + 10);  // Healthy plants grow better
        }

        public void grow() {
            if (stage < 4) {
                growthTime++;
                if (growthTime >= (stage + 1) * 10) { // Each stage takes more time
                    stage++;
                    growthTime = 0;  // Reset growth time for next stage
                }
            }
        }

        public void fertilize() {
            health = Math.min(100, health + 15);  // Fertilizing boosts plant health
        }

        public void harvest() {
            // Reward the player with points or resources upon harvesting
            JOptionPane.showMessageDialog(null, "Congratulations! You have harvested your plant.");
        }

        // Pass time for plant growth and changes
        public void passTime() {
            if (stage < 4) {
                growthTime++;
                if (growthTime >= (stage + 1) * 5) {
                    grow();
                }
            }
            // Simulate natural decay or other events (rain, storm, etc.)
            if (waterLevel > 0) waterLevel--;
            if (health < 100) health++;
        }

        // Getter methods
        public int getStage() {
            return stage;
        }

        public int getHealth() {
            return health;
        }

        public int getWaterLevel() {
            return waterLevel;
        }

        public int getGrowthTime() {
            return growthTime;
        }

        public Color getColor() {
            switch (stage) {
                case 1: return Color.GREEN;  // Sprout
                case 2: return new Color(34, 139, 34);  // Vegetative
                case 3: return Color.YELLOW;  // Flowering
                default: return Color.GRAY;  // Seed / Harvest
            }
        }

        public int getWidth() {
            return 50 + stage * 20;  // Plant width increases with stages
        }

        public int getHeight() {
            return 50 + stage * 30;  // Plant height increases with stages
        }
    }
}
