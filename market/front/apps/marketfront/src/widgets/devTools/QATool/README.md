- Actions

[x] Add Filter
[x] Remove Filter
[ ] Change Filter

[x] Add Product
[x] Remove Product
[ ] Search Product
[ ] Search Product Success
[ ] Search Product Failure

[ ] Add Product to Cart
[ ] Add All Products to Cart
[ ] Clear Cart

[ ] Save settings
[ ] Load settings

- Types

type Filter = {
    id: string,
    value: string,
};

type Item = {
    product: ?{
        offerId: string,
        sku?: string,
        productId?: string,
    },
    filters: Filter[],
    status?: 'loading' | 'success' | 'failure',
};
