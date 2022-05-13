# FirstRohitLibrarypublic class AllItemsAdapter extends RecyclerView.Adapter<AllItemsAdapter.MyViewHolder> {
    Context context;
    int type = 0;
    public static final int SPAN_COUNT_ONE = 1;
    public static final int SPAN_COUNT_FIVE = 5;

    private static final int VIEW_TYPE_SMALL = 1;
    private static final int VIEW_TYPE_BIG = 2;

    private GridLayoutManager mLayoutManager;
    private OnItemClickListener mClickListener;

    public interface OnItemClickListener {
        void onItemCate(View v, int position, TextView txt, String name);
    }

    public void setOnCateItemClickListener(final OnItemClickListener mClickListener) {
        this.mClickListener = mClickListener;
    }

    public AllItemsAdapter(Context context1, GridLayoutManager layoutManager) {
        this.context = context1;
        mLayoutManager = layoutManager;
    }

    @NonNull
    @Override
    public MyViewHolder onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {
        View view;
        if (viewType == VIEW_TYPE_BIG) {
            view = LayoutInflater.from(parent.getContext()).inflate(R.layout.items_linear_all_products, parent, false);
        } else {
            view = LayoutInflater.from(parent.getContext()).inflate(R.layout.items_all_products, parent, false);
        }
        return new MyViewHolder(view, viewType);
    }

    @Override
    public int getItemViewType(int position) {
        int spanCount = mLayoutManager.getSpanCount();
        if (spanCount == SPAN_COUNT_ONE) {
            return VIEW_TYPE_BIG;
        } else {
            return VIEW_TYPE_SMALL;
        }
    }

    @Override
    public void onBindViewHolder(@NonNull MyViewHolder holder, @SuppressLint("RecyclerView") int position) {

        if (holder.lyGridLayout!=null){
            holder.lyGridLayout.setOnClickListener(new View.OnClickListener() {
                @Override
                public void onClick(View view) {
                    Toast.makeText(context, "click" + position, Toast.LENGTH_SHORT).show();
                }
            });
        }
        if (holder.lyLinear!=null){
            holder.lyLinear.setOnClickListener(new View.OnClickListener() {
                @Override
                public void onClick(View view) {
                    Toast.makeText(context, "click" + position, Toast.LENGTH_SHORT).show();
                }
            });
        }
        holder.itemView.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Toast.makeText(context, "click" + position, Toast.LENGTH_SHORT).show();
            }
        });
    }

    @Override
    public int getItemCount() {
        return 6;
    }

    public class MyViewHolder extends RecyclerView.ViewHolder {
        LinearLayoutCompat lyGridLayout, lyLinear;

        public MyViewHolder(@NonNull View itemView, int viewType) {
            super(itemView);
            if (viewType == VIEW_TYPE_BIG) {
                lyLinear = itemView.findViewById(R.id.lyLinear);
            } else {
                lyGridLayout = itemView.findViewById(R.id.lyGridLayout);
            }
        }
    }
}

public class MainActivity extends AppCompatActivity {
    RecyclerView recyclerView_cateall;
    AllItemsAdapter allItemsAdapter;
    private GridLayoutManager gridLayoutManager;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        gridLayoutManager = new GridLayoutManager(this, SPAN_COUNT_FIVE);
        allItemsAdapter = new AllItemsAdapter(this, gridLayoutManager);
        recyclerView_cateall = findViewById(R.id.recylerViewAllItems);
        recyclerView_cateall.setAdapter(allItemsAdapter);
        recyclerView_cateall.setLayoutManager(gridLayoutManager);
        findViewById(R.id.btnClick).setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                setRecylerView();
            }
        });
    }

    void setRecylerView() {
        if (gridLayoutManager.getSpanCount() == SPAN_COUNT_ONE) {
            gridLayoutManager.setSpanCount(SPAN_COUNT_FIVE);
        } else {
            gridLayoutManager.setSpanCount(SPAN_COUNT_ONE);
        }
        allItemsAdapter.notifyItemRangeChanged(0, allItemsAdapter.getItemCount());
    }

}


<?xml version="1.0" encoding="utf-8"?>
<androidx.appcompat.widget.LinearLayoutCompat xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:id="@+id/lyGridLayout"
    android:layout_marginTop="20dp">

    <com.google.android.material.card.MaterialCardView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_margin="8dp"
        android:clickable="true"
        android:focusable="true"
        app:cardCornerRadius="4dp">

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:minHeight="138dp"
            android:orientation="vertical">

            <androidx.appcompat.widget.LinearLayoutCompat
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:background="@android:color/transparent"
                android:contentDescription="Card Image"
                android:scaleType="centerCrop"
                app:backgroundTint="@color/material_on_surface_emphasis_medium"
                app:backgroundTintMode="add">

                <androidx.appcompat.widget.LinearLayoutCompat
                    android:layout_width="match_parent"
                    android:layout_height="wrap_content"
                    android:orientation="vertical"
                    android:scaleType="centerCrop">

                    <androidx.appcompat.widget.AppCompatTextView
                        android:layout_width="match_parent"
                        android:layout_height="wrap_content"
                        android:layout_marginTop="10dp"
                        android:padding="2dp"
                        android:gravity="center"
                        android:text="Available Quantity"/>
                    <androidx.appcompat.widget.AppCompatTextView
                        android:layout_width="match_parent"
                        android:layout_height="wrap_content"
                        android:textColor="@color/white"
                        android:textStyle="bold"
                        android:layout_marginBottom="10dp"
                        android:gravity="center"
                        android:text="2"/>
                </androidx.appcompat.widget.LinearLayoutCompat>
            </androidx.appcompat.widget.LinearLayoutCompat>
            <TextView
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:padding="4dp"
                android:textColor="@color/black"
                android:layout_marginTop="5dp"
                android:text="1 Lt Milkymis Ghee"/>
            <TextView
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:textColor="@color/black"
                android:layout_marginLeft="10dp"
                android:textStyle="bold"
                android:text="dfghdh"/>
        </LinearLayout>
    </com.google.android.material.card.MaterialCardView>

</androidx.appcompat.widget.LinearLayoutCompat>


<?xml version="1.0" encoding="utf-8"?>
<androidx.appcompat.widget.LinearLayoutCompat xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:id="@+id/lyLinear"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:background="#FFFFFF"
    android:orientation="vertical">
    <androidx.appcompat.widget.LinearLayoutCompat
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal">
        <com.google.android.material.card.MaterialCardView
            android:layout_width="100dp"
            android:layout_height="100dp"
            android:layout_marginLeft="20dp"
            android:layout_marginTop="20dp"
            android:layout_marginBottom="20dp"
            app:cardBackgroundColor="@color/teal_200">
            <RelativeLayout
                android:layout_width="match_parent"
                android:layout_height="match_parent">
                <TextView
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:textColor="@color/white"
                    android:textStyle="bold"
                    android:textSize="18dp"
                    android:layout_centerInParent="true"
                    android:text="FO"/>
            </RelativeLayout>
        </com.google.android.material.card.MaterialCardView>

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:gravity="center_vertical"
            android:orientation="vertical"
            android:padding="16dp">

            <TextView
                android:id="@+id/title_big"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_marginBottom="4dp"
                android:textSize="15dp"
                android:textStyle="bold"
                android:textColor="@color/black"
                android:text="Fortune 15 Ltr"
                android:textAppearance="@style/TextAppearance.AppCompat.Medium" />

            <TextView
                android:id="@+id/tv_info"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:text="tfghsrfdh"
                android:textAppearance="@style/TextAppearance.AppCompat.Small" />
            <TextView
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:text="Barcode : 67627566754"
                android:textAppearance="@style/TextAppearance.AppCompat.Small" />

        </LinearLayout>
    </androidx.appcompat.widget.LinearLayoutCompat>

    <View
        android:layout_width="match_parent"
        android:layout_height="1dp"
        android:background="@android:color/darker_gray"/>
</androidx.appcompat.widget.LinearLayoutCompat>
