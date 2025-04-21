# Marimo in Jekyll (markdoww)

This page shows how to use [Marimo notebooks](https://docs.marimo.io/)
in a Jekyll website using pure HTML.

See this post for more information.

## Using iframes

Iframes open a notebook directly into your webpage.

<marimo-iframe>
    <pre>
    import matplotlib.pyplot as plt
    import numpy as np
    import marimo as mo
    </pre>

    <pre>
    mo.md("Taken from the [matplotlib doc](https://matplotlib.org/stable/gallery/lines_bars_and_markers/bar_stacked.html)")
    </pre>

    <pre>
    # data from https://allisonhorst.github.io/palmerpenguins/
    species = (
        "Adelie\n $\\mu=$3700.66g",
        "Chinstrap\n $\\mu=$3733.09g",
        "Gentoo\n $\\mu=5076.02g$",
    )
    weight_counts = {
        "Below": np.array([70, 31, 58]),
        "Above": np.array([82, 37, 66]),
    }
    </pre>

    <pre>
    width = 0.5

    fig, ax = plt.subplots()
    bottom = np.zeros(3)

    for boolean, weight_count in weight_counts.items():
        p = ax.bar(species, weight_count, width, label=boolean, bottom=bottom)
        bottom += weight_count

    ax.set_title("Number of penguins with above average body mass")
    ax.legend(loc="upper right")

    plt.show()
    </pre>
</marimo-iframe>

## Using buttons

Buttons will open a notebook in the marimo playground.

<marimo-button>

    <pre>
    import matplotlib.pyplot as plt
    import numpy as np
    import marimo as mo

    import matplotlib.cbook as cbook

    # Load a numpy record array from yahoo csv data with fields date, open, high,
    # low, close, volume, adj_close from the mpl-data/sample_data directory. The
    # record array stores the date as an np.datetime64 with a day unit ('D') in
    # the date column.
    price_data = cbook.get_sample_data('goog.npz')['price_data']
    price_data = price_data[-250:]  # get the most recent 250 trading days

    delta1 = np.diff(price_data["adj_close"]) / price_data["adj_close"][:-1]

    # Marker size in units of points^2
    volume = (15 * price_data["volume"][:-2] / price_data["volume"][0])**2
    close = 0.003 * price_data["close"][:-2] / 0.003 * price_data["open"][:-2]

    fig, ax = plt.subplots()
    ax.scatter(delta1[:-1], delta1[1:], c=close, s=volume, alpha=0.5)

    ax.set_xlabel(r'$\Delta_i$', fontsize=15)
    ax.set_ylabel(r'$\Delta_{i+1}$', fontsize=15)
    ax.set_title('Volume and percent change')

    ax.grid(True)
    fig.tight_layout()

    plt.show()

    mo.md("Taken from the [matplotlib doc](https://matplotlib.org/stable/gallery/lines_bars_and_markers/barh.html)")
    </pre>

</marimo-button>

[SOURCE](https://github.com/Remi-Gau/jekyll-primer/blob/main/marimo_md.md)

<!-- Needed to render Marimo in HTML. -->
<script src="https://cdn.jsdelivr.net/npm/@marimo-team/marimo-snippets@1"></script>
