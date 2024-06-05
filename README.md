# Lista-09
Atividade de Programação de Soluções Computacionais



import java.util.Scanner;

abstract class PersonagemDragonBall {
    protected String nome;
    protected int idade;
    protected String sexo;
    protected String temporada;
    protected int ki;
    protected String poderEspecial;

    public PersonagemDragonBall(String nome, int idade, String sexo, String temporada, int ki, String poderEspecial) {
        this.nome = nome;
        this.idade = idade;
        this.sexo = sexo;
        this.temporada = temporada;
        this.ki = ki;
        this.poderEspecial = poderEspecial;
    }

    public abstract int calcularPoder();

    @Override
    public String toString() {
        return "Nome: " + nome + ", Idade: " + idade + ", Sexo: " + sexo + ", Temporada: " + temporada + ", Ki: " + ki + ", Poder Especial: " + poderEspecial;
    }
}

interface Transformavel {
    String transformar(int nivel);
}

class Terraqueo extends PersonagemDragonBall {
    private String pais;
    private String cidade;

    public Terraqueo(String nome, int idade, String sexo, String temporada, int ki, String poderEspecial, String pais, String cidade) {
        super(nome, idade, sexo, temporada, ki, poderEspecial);
        this.pais = pais;
        this.cidade = cidade;
    }

    @Override
    public int calcularPoder() {
        return ki;
    }

    @Override
    public String toString() {
        return super.toString() + ", País: " + pais + ", Cidade: " + cidade;
    }
}

class Sayajin extends PersonagemDragonBall implements Transformavel {
    private int nivelMaximoSSJ;
    private boolean temRabo;

    public Sayajin(String nome, int idade, String sexo, String temporada, int ki, String poderEspecial, int nivelMaximoSSJ, boolean temRabo) {
        super(nome, idade, sexo, temporada, ki, poderEspecial);
        this.nivelMaximoSSJ = nivelMaximoSSJ;
        this.temRabo = temRabo;
    }

    @Override
    public int calcularPoder() {
        return (int) (ki * (1 + nivelMaximoSSJ * 0.1));
    }

    @Override
    public String transformar(int nivel) {
        if ((nivel >= 1 && nivel <= 3) || (nivel >= 4 && nivel <= 5 && (nome.equals("Goku") || nome.equals("Vegeta")))) {
            return nome + " transformou para super sayajin nível " + nivel;
        } else {
            return "Não foi possível transformar esse sayajin";
        }
    }

    @Override
    public String toString() {
        return super.toString() + ", Nível Máximo SSJ: " + nivelMaximoSSJ + ", Tem Rabo: " + temRabo;
    }
}

class Namekuseijin extends PersonagemDragonBall {
    private int quantidadeEsferas;
    private boolean podeCurar;

    public Namekuseijin(String nome, int idade, String sexo, String temporada, int ki, String poderEspecial, int quantidadeEsferas, boolean podeCurar) {
        super(nome, idade, sexo, temporada, ki, poderEspecial);
        this.quantidadeEsferas = quantidadeEsferas;
        this.podeCurar = podeCurar;
    }

    @Override
    public int calcularPoder() {
        return (int) (ki * (1 + (podeCurar ? 0.2 : 0)));
    }

    public String fazerDesejo(String desejo) {
        return desejo.replace("vida", "nama").replace("poder", "balta").replace("mundo", "kaio");
    }

    @Override
    public String toString() {
        return super.toString() + ", Quantidade de Esferas: " + quantidadeEsferas + ", Pode Curar: " + podeCurar;
    }
}

class PersonagemFactory {
    public static PersonagemDragonBall criarPersonagem(String nome) {
        switch (nome) {
            case "Kuririn":
                return new Terraqueo("Kuririn", 35, "Masculino", "Temporada 1", 2000, "Kienzan", "Terra", "Cidade do Leste");
            case "Goku":
                return new Sayajin("Goku", 42, "Masculino", "Temporada 1", 9000, "Kamehameha", 5, true);
            case "Gohan":
                return new Sayajin("Gohan", 23, "Masculino", "Temporada 1", 8000, "Masenko", 3, true);
            case "Dendê":
                return new Namekuseijin("Dendê", 25, "Masculino", "Temporada 1", 3000, "Curar", 7, true);
            default:
                throw new IllegalArgumentException("Personagem desconhecido");
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Escolha o personagem a criar (Kuririn, Goku, Gohan, Dendê):");
        String escolha = scanner.nextLine();

        PersonagemDragonBall personagem = PersonagemFactory.criarPersonagem(escolha);

        System.out.println("Personagem criado:");
        System.out.println(personagem);

        if (personagem instanceof Sayajin) {
            Sayajin sayajin = (Sayajin) personagem;
            System.out.println(sayajin.transformar(5));
        }

        if (personagem instanceof Sayajin) {
            Sayajin sayajin = (Sayajin) personagem;
            String transformacaoGohan = sayajin.transformar(5);
            if (transformacaoGohan.contains("Não foi possível")) {
                transformacaoGohan = sayajin.transformar(3);
            }
            System.out.println(transformacaoGohan);
        }

        if (personagem instanceof Namekuseijin) {
            Namekuseijin namekuseijin = (Namekuseijin) personagem;
            String desejo = "Desejo vida e poder para o mundo";
            System.out.println("Desejo em Namekusei: " + namekuseijin.fazerDesejo(desejo));
        }
    }
}











Print da execução:
![image](https://github.com/barbieags/Lista-09/assets/166566797/78fe9af0-9e4d-4e55-afe8-b00e738afdc5)

